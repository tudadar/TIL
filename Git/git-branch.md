# Git 특정 브랜치 clone

실무 작업중에 특정 브랜치를 내려받아야할 필요가 있었다.

그래서 찾아보았다.

clone 뒤에 --branch [내려받을 branch명] [Repository_URL]

```
git clone --branch hotfix/1024 [Repository_URL]
```