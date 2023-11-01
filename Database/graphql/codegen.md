# graphql codegen 사용하기

업무중에 db를 활용하는 작업이

아직까지는 생각보다 없는거 같아서

가끔 codegen 사용법을 까먹는일이 생겨서 적는거임

내가 참여중인 사내 플젝기준이니 따라해도 안될수 있음

```sql
mutation deleteQuotationByPk($id: uuid!) {
  update_rc_quotation_by_pk(
    pk_columns: { id: $id }
    _set: { deleted_at: "now()" }
  ) {
    id
  }
}
```

이런 쿼리가 있다고 합시다.

.graphql 확장자의 파일을 만들어서

쿼리를 그대로 넣은뒤

콘솔창에서 turbo codegen을 입력하거나

빌드를 하게되면 쿼리를 사용할수있게 만들어줌