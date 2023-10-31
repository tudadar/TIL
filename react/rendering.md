# 실무중에 발생한 React 랜더링 이슈

react ui 라이브러리인 mui datagrid로 된 테이블이 mui의 업데이트로 인해 정상적으로 작동을 안해서

새로 만드는 작업을 했었다.

테이블에 데이터를 출력하는 기능이 있는데

기존에는 컴포넌트 분리 없이 한페이지에 테이블과 그외 데이터들을 출력했었는데

이번엔 테이블을 따로 분리하게 되었다.

top down 방식이 아니라 반대로 작업을 하게되어서 어려운점이 많았고 팀장님의 도움도 많이 받았다.

테이블을 따로 분리하면서 페이지 로드시 출력되는 쿼리를 수정했는데

아래는 컴포넌트 분리 없이 한개의 페이지로 처리하는 기존쿼리이다.

```ts
const { data, loading, error } = useSelectQuotationByPkQuery({
    variables: {
      id: id,
    },
    skip: id === '',
  });
  useEffect(() => {
    if (data && !loading) {
      setIssued(data.rc_quotation_by_pk?.issued_at ? true : false);
      formik.resetForm({
        values: {
          clientName: data.rc_quotation_by_pk?.client_name ?? '',
          data: data.rc_quotation_by_pk?.data as CQuoteData,
          companySeal:
            _.head<any>(
              data.rc_quotation_by_pk?.rc_company.rc_company_attachments,
            )?.key ?? '',
        },
      });

      let id = newId;
      const rows = data.rc_quotation_by_pk?.data.cars.map(
        (car: {
          model: string;
          term: number;
          termUnit: string;
          qty: number;
          unitPrice: number;
        }) => {
          return {
            id: id++,
            model: car.model,
            term: car.term,
            termUnit: car.termUnit,
            qty: car.qty,
            unitPrice: car.unitPrice,
          };
        },
      );
      setCarRows(rows);
      setSavedCarRows(rows);
      setNewId(id);
    }
  }, [data, loading]);
```

아래는 이 코드를 컴포넌트별로 분리한것이다.

```ts
// 테이블 컴포넌트의 쿼리
  const { data, loading } = useSelectQuotationByPkQuery({
    variables: {
      id: id,
    },
    skip: id === '',
  });
  useEffect(() => {
    if (data && !loading) {
      let id = newId;
      const rows = data.rc_quotation_by_pk?.data.cars.map(
        (car: {
          model: string;
          term: number;
          termUnit: string;
          qty: number;
          unitPrice: number;
        }) => {
          return {
            id: id++,
            model: car.model,
            term: car.term,
            termUnit: car.termUnit,
            qty: car.qty,
            unitPrice: car.unitPrice,
          };
        },
      );
      props.append(rows);
      handleChange({ carRows: props.getValues('carRows') }, event); // 데이터 불러올때 변수에 값 저장
    }
  }, [data, loading]);
```

```ts
// 그외 데이터 컴포넌트
  const { data, loading, error } = useSelectQuotationByPkQuery({
    variables: {
      id: id,
    },
    skip: id === '',
  });
  useEffect(() => {
    if (data && !loading && !isRendered) {
      setIssued(data.rc_quotation_by_pk?.issued_at ? true : false);
      formik.resetForm({
        values: {
          clientName: data.rc_quotation_by_pk?.client_name ?? '',
          data: data.rc_quotation_by_pk?.data as CQuoteData,
          companySeal:
            _.head<any>(
              data.rc_quotation_by_pk?.rc_company.rc_company_attachments,
            )?.key ?? '',
        },
      });
    }
  }, [data, loading]);
```

보통 렌더링을 페이지로드시 1회만 할려면 코드의 마지막줄 [data, loading]를

비워둬서 []으로 하는 방법이 기본적으로 많이 쓰는 방법인데

이 경우에는 해당이 안되었다.

이유는 화면이 로딩이 되기전에 데이터를 출력을 시도해서 데이터 없이 출력이 된다.

해결방법은 지금 생각해보면 별거 아니라 생각되는데

아래와 같이 처리했다.

```ts
// 테이블 컴포넌트의 쿼리
const [isRendered, setIsRendered] = useState(false);

  const { data, loading } = useSelectQuotationByPkQuery({
    variables: {
      id: id,
    },
    skip: id === '',
  });
  useEffect(() => {
    if (data && !loading) {
      let id = newId;
      const rows = data.rc_quotation_by_pk?.data.cars.map(
        (car: {
          model: string;
          term: number;
          termUnit: string;
          qty: number;
          unitPrice: number;
        }) => {
          return {
            id: id++,
            model: car.model,
            term: car.term,
            termUnit: car.termUnit,
            qty: car.qty,
            unitPrice: car.unitPrice,
          };
        },
      );
      props.append(rows);
      handleChange({ carRows: props.getValues('carRows') }, event); // 데이터 불러올때 변수에 값 저장
      setIsRendered(true); // 랜더링을 1회만 하기 위한 설정
    }
  }, [data, loading]);
```

이렇게 처리를 하면

isRendered 상태가 true가 될 때만 useEffect 훅이 실행되고

페이지 로드 시 isRendered 상태는 false로 초기화되므로, 랜더링은 1회만 실행됨

