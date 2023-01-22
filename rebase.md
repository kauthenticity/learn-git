## rebase

### rebase란

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FLIudr%2FbtqCpQU8cPT%2FPM34NEHFCUZndlhXxt55n0%2Fimg.png" width="400px">

- master로 `rebase`한다는 것은, c4에서의 `patch`를 c3에 적용시키는 것
  - `patch`란, `diff`에 의해 생성된 두 파일의 차이를 나타내는 파일

### rebase 작동 예시

```shell
git checkout experiment
git rebase master
```

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FSVKNl%2FbtqCqNcQPaP%2Fijwz6OKTfr2mGke0o6lXM1%2Fimg.png" width="400px">

1. 공통 조상 커밋부터 `checkout`한 브랜치가 가리키는 커밋까지의 `diff`를 만든다.
2. `HEAD`가 `rebase`시킬 `branch`를 가리키도록 한다.
3. 이제 `HEAD`에 `diff`를 차례대로 적용한다.
   - 이때 `commit`을 만들면서 `HEAD` 포인터를 하나씩 이동시킨다.
4. `experiment`를 `HEAD`가 가리키는 곳을 가리키도록 한다.

이 과정까지 거치면 `master`는, 본인의 마지막 커밋을 가리키게 된다.
따라서 experiment로 `fast-forward` 시킨다.

```shell
git checkout master
git merge experiment
```

### rebase의 워험성

> 🚧 Do not rebase commits that exist outside your repository and that people may have based work on

- 내가 커밋한 걸 원격 저장소에 `push`하고, 팀원이 그 커밋을 `pull`받았다.
- 내가 그 커밋을 `rebase`해서, `push`하면, 팀원은 `push`전에, 원격 저장소를 `pull` 하여 `merge` 한 후에야 `push`할 수 있다.
- 팀원이 `push`한 걸 `pull`하면, `merge`한 그 커밋과 `rebase` 커밋 두 개가 존재하게 된다.
- 두 커밋은 커밋 번호만 다를 뿐, 커밋 내용, 날짜, 메시지가 완전히 똑같은 커밋이므로 혼란을 야기한다.
