---
layout: post
title: "git status 시 보이는 파일 수정 내역에서 특정 파일 제외하기"
author: "Soy-A"
comments: true
tags:
- Git
---

작업을 하다보면 종종 작업 환경과 관련된 파일이 git 내역에 포함되어있을 때가 있다.

이 경우, 팀원의 작업 환경과 내 로컬의 작업 환경이 달라 계속해서 나의 환경 변경 내역이 git status의 수정된 파일 목록에 잡힌다.

이러한 파일은 미리 .gitignore에 포함시키고 시작하는 것이 최선이지만, 이미 프로젝트가 많이 진행되어 큰 의미가 없을 경우에는 내 수정내역이 이력에 반영되지 않도록 조심하는 방법 밖에는 없다.

git add .를 사용하지 못하고, 매번 파일 이름을 하나하나 입력해서 변경 사항을 추가하는 것은 너무나도 귀찮은 일.

아래와 같은 명령을 사용하면 특정 파일의 변경사항을 없는 것으로 간주하도록 할 수 있다.

```
$ git update-index --assume-unchanged 파일명
$ git update-index --no-assume-unchanged 파일명    // 다시 변경내역 추가
$ git ls-files -v | grep ^h    // unchanged로 지정된 파일 보기
```

참조: [https://blog.outsider.ne.kr/817](https://blog.outsider.ne.kr/817)
