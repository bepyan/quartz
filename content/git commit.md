
## empty commit

CLI를 통해서 빈 커밋 올리는 방법이다.

```shell
git commit --allow-empty -m "empty commit"
```


## skip-checks

github action을 수행하지 않고 싶을 땐 아래 같이 커밋 메시지를 추가하면 된다.

```
git commit --allow-empty -m "empty commit
>
>
skip-checks: true"
```

https://docs.github.com/en/enterprise-server@3.9/pull-requests/collaborating-with-pull-requests/collaborating-on-repositories-with-code-quality-features/about-status-checks#skipping-and-requesting-checks-for-individual-commits