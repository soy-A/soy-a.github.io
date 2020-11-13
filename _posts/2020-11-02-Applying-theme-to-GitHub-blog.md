---
layout: post
title: GitHub 블로그에 테마 적용하기
comments: true
tags:
- Jekyll
- 블로그
- GitHub
---

예전 학교 수업에서, GitHub를 사용하는 법을 배우며 GitHub Pages를 사용하는 법도 배웠었다. 그때에는 Jekyll를 설치하지 않고 바로 내 repository에 가져와 사용했었는데, 이번 기회에 Jekyll을 설치해 내 GitHub 블로그를 관리해보기로 했다.

하지만 항상 그렇듯, 쉬운 블로그 설명들과는 달리 내 컴퓨터에서는 안되는 것 투성이다.

이 포스팅에서는 내가 Jekyll을 사용해 블로그 테마를 적용하며 마주쳤던 오류들을 다뤄보고자 한다.

-------

## Jekyll 설치하기<br/>
Jekyll을 설치하는 과정부터 쉽지 않았다.
```bash
$ gem install bundler jekyll
```
이 명령어를 통해 Jekyll을 설치하고자 했지만, permission 에러가 발생했다.

별 기대 없이 sudo명령도 해보았으나, 통할리가 만무.

알아보니, ruby에 관련된 에러였다.

맥북에는 ruby가 설치되어있다는 말만 철썩같이 믿고 Jekyll설치를 진행했으나, 이 시스템 ruby로는 설치를 진행할 수 없어 ruby관리자인 rbenv를 이용해 ruby를 설치해주어야 했다.

```bash
$brew install rbenv
$rbenv install 2.6.6 // 버전 선택 및 설치
$rbenv global 2.6.6 // 설치된 버전을 시스템이 기본적으로 사용하도록 함
```
이렇게 설치 후, rbenv 초기화도 해주어야 한다.
```bash
$rbenv init
```
위의 명령을 실행하면, ~/.bash_profile에 eval "$(rbenv init -)"를 쓰라는 지시사항이 나온다.

```bash
$vi ~/.bash_profile
```
vi 에디터로 파일을 열어서 eval "$(rbenv init -)"를 적어주면 된다.

터미널을 재실행 하는 건 번거로우니 source명령어로 마무리해주었다.

드디어 문제없이 Jekyll설치가 가능해졌다.

하지만 곧 또다른 문제를 만나게 되었으니...

------

## Jekyll 테마 적용

Jekyll을 이용하여 내가 원하는 블로그를 커스토마이징 할 수 있지만, 그건 너무 번거로워 테마를 적용하기로 했다.

깃허브에 올라와있는 수많은 테마들 중, lanyon테마가 가장 마음에 들었다.

lanyon의 repository를 clone하여 내 로컬로 옮겨오고, Jekyll을 실행시켜보았으나 새빨간 오류메세지와 함께 실행이 되지 않았다.

>Dependency Error: Yikes! It looks like you don't have jekyll-paginate or one of its dependencies installed. In order to use Jekyll as currently configured, you'll need to install this gem. The full error message from Ruby is: 'cannot load such file -- jekyll-paginate' If you run into trouble, you can find helpful resources at http://jekyllrb.com/help/!

jekyll-paginate가 설치되지 않아 발생한 문제인가 싶어
```bash
$gem install jekyll-paginate
```
명령어를 이용하여 설치해보았으나, 같은 오류가 반복되었다.

결국 Gemfile을 수정하는 방법으로 이 문제를 해결할 수 있었는데, Gemfile을 열어 gem "jekyll-paginate", "~> 1.1.0"을 추가 해주니 잘 실행되었다.

사실 잘 실행되었다고 적었지만, 한 가지의 문제가 더 발생하고있었다. 

실행은 되지만 Build Warning 메시지가 뜨며 새하얀 화면만이 뜨는 문제였다.
>Build Warning: Layout 'home' requested in index.markdown does not exist.

적혀있는대로 index.markdown 파일에 layout으로 설정되어있는 home이 존재하지 않아서 발생하는 오류이다. 

우리가 가지고있는 layout의 이름은 Home이므로 index.markdown의 내용을 다음과 같이 수정해주면 된다.
>---\nlayout: default\ntitle: Home\n---

이로써 테마적용을 완벽히 끝낼 수 있었다. 

생각보다 다양한 오류들이 발생했지만, 모든 오류에는 원인이 있는 법이다. 

앞으로도 수없이 만날 상황들이니 더 자주 부딪히며 익숙해지는 수 밖에 없겠다.
