---
layout: post
title: "GitHub 블로그에 css 적용이 안될 때"
author: "Soy-A"
comments: true
tags:
- Jekyll
- 블로그
- GitHub
- css
---

GitHub블로그를 만들기 위해 로컬 컴퓨터에서 jekyll 서버를 돌렸을 때에는 테마 적용이 예쁘게 되었다.

하지만 git push를 이용해 GitHub pages로 파일들을 옮겨주자 적용한 테마는 어디로 사라지고 투박한 글씨들만 남아있었다.

한숨 한 번 쉬고 다시 시작한 원인찾기!

-------

## 상대경로와 절대경로

<br/>
구글링을 해보니, css가 적용되지 않는 이유로 상대경로와 절대경로에 대한 내용이 많았다.

보통은 내 닉네임.github.io라는 이름을 가진 repository를 사용해 블로그를 만들지만, 이와 다른 프로젝트 이름으로 블로그를 만든 경우 생기는 문제였다.

본인의 닉네임으로 블로그를 만든 경우는 절대경로에 해당되는데, 이 경우에는 config.yml파일의 url은 블로그 주소를, baseurl은 ''을 적어주어야 한다.

프로젝트 블로그를 만든 경우에는, baseurl에 /프로젝트이름을 적어줘 상대경로를 지정해주어야 한다.

블로그에 적용될 테마 파일들의 경로가 프로젝트 페이지로 올바르게 들어가도록 해주는 것이다.

하지만 내 블로그는 프로젝트 페이지가 아니었기 때문에 내 경우에 해당되는 이야기는 아니었다.

따라서 몇몇 사례들을 더 찾아보아야만 했다...

---

## 대소문자

<br/>
보통 css가 적용되지 않는 것은 경로의 문제가 대부분인듯 싶었다.

파일 확장자가 대문자로 쓰여있는 경우에도 에러가 날 수 있다는 사례를 찾았지만, 내 파일들은 모두 소문자였다.

곰곰히 생각해보니 내 닉네임이 대문자여서 발생한 에러일 수 있겠다 싶어 이것저것 시도해보았지만 별 소용이 없었다.

---

## http와 https(Mixed content error)

<br/>
드디어 찾았다!

내 투박한 블로그 페이지에서 검사버튼을 눌러보니, 여러 오류 메시지를 확인할 수 있었다.
>Mixed Content: The page at 'https://soy-a.github.io/' was loaded over HTTPS, but requested an insecure stylesheet 'http://soy-a.github.io/public/css/poole.css'. This request has been blocked; the content must be served over HTTPS.

http와 https에 대한 오류 메시지인듯 싶어 검색해보니 역시나였다.

내 깃헙 블로그 페이지는 https로 되어있는데, config.yml파일의 url에는 http로 적어줬던 것이다.

url을 http로 잘못 적어준 탓에, 블로그가 css파일들을 http로 불러오려고 하며 Mixed-content error가 발생한 것이었다.

>Mixed-content error는 https 페이지에서 http의 리소스를 요청할때 보안의 취약점을 방어하기 위해서 발생하는 에러이다.

역시 답은 에러메시지에 있었다.

며칠 동안 삽질해본 끝에, 드디어 예쁜 블로그를 만들어내는데에 성공했다.

열심히 꾸미고 다듬어보아야겠다.
