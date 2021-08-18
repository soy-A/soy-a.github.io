---
layout: post
title: "Amazon RDS mysql 데이터를 csv 파일로 내보내기"
author: "Soy-A"
comments: true
tags:
- mysql
---
Amazon RDS 서버에서 mysql을 사용하면, FILE 권한이 주어지지 않는다.

따라서 쿼리 결과를 csv로 내보내는 "SELECT ... INTO OUTFILE" 쿼리 또한 실행할 수 없다.

하지만 mysql 커맨드라인에서 select 작업을 수행하고 그 결과가 csv 파일로 출력되도록 파이핑하면 원하던 결과를 얻을 수 있다.

```
$ mysql -u username -p --host=rdshostname --port=rdsport --batch 
  -e "select * from yourtable" 
  | sed 's/\t/","/g;s/^/"/;s/$/"/;s/\n//g' > yourlocalfilename
```
sed가 없다면, Perl 또는 다른 스크립트 언어를 사용해 출력을 csv로 변환할 수 있다.

```
mysql -u username -p --host=rdshostname --port=rdsport --batch 
  -e "select * from yourtable" 
  | perl -F"\t" -lane 'print join ",", map {s/"/""/g; /^[\d.]+$/ ? $_ : qq("$_")} @F ' > yourlocalfilename
```
필드가 이미 지정되어있다면 다음과 같은 명령어도 가능하다.
```
mysql -uroot -ppassword --database=dbtest
  -e "select concat(field1,',',field2,',',field3) FROM tabletest" > tabletest.csv
```

출처: <https://stackoverflow.com/questions/9536224/exporting-a-table-from-amazon-rds-into-a-csv-file>
