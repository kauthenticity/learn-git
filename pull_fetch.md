## pull and fetch

### pull과 fetch의 차이점

- `pull`을 하면 원격 저장소의 내용을 가져와 자동으로 `merge`까지 한다.
- `fetch`를 하면, 원격 저장소에서 내용을 가져오기만 하고 `merge`가 일어나지는 않는다.

### fetch를 하면

<img src="https://backlog.com/git-tutorial/kr/img/post/stepup/capture_stepup3_2_1.png" width="400px">

- `fetch`를 하면 `FETCH_HEAD`라는 브랜치가 생기고, 얘가 원격 저장소의 마지막 커밋을 가리키게 된다.

<img src="https://backlog.com/git-tutorial/kr/img/post/stepup/capture_stepup3_2_2.png" width="400px">

- 이때 `fetch`한 내용을 `local`의 `master`에 합치고 싶으면
  ```bash
  git checkout master
  git merge FETCH_HEAD
  ```
