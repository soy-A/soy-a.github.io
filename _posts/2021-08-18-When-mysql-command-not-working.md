---
layout: post
title: "mysql 명령어가 작동하지 않을 때"
author: "Soy-A"
comments: true
tags:
- mysql
---
이전에 bitnami로 mamp를 설치해두고는 방치해 두었다.

최근 mysql을 사용할 일이 있어 그 때 설치한 mysql을 사용하고자 했으나, $mysql 명령어가 먹히지 않았다.

분명 처음에 설치하고나서도 같은 문제로 헤메었던 터라, 다음에 또 까먹을 나를 위해  적어두는 글...

---

```
cd /Applications/mampstack-8.0.6-0//mysql/bin/    // mysql 설치 경로
sudo ./mysql -uroot –p
```

mysql 설치 경로를 환경 변수에 등록해두면 $./mysql 명령만으로도 실행이 가능하다.
