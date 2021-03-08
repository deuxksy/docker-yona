# docker-yona

**docker-yona**는 **git** 기반 협업 프레임워크 [Yona](http://yona.io)를 사용하기 편리하게 docker 컨테이너로 만든 컨테이너 이미지 입니다.

## 1.adminer

DB 관리를 위해서

## 2.mariadb

RDB

## 3.yona

Windows 기반의 docker 에서 하면 아래와 같은 문제가 발생함

```bash
standard_init_linux.go:219: exec user process caused: no such file or directory
```

CRLF 문제라고 하는되 어느 파일에서 발생 한건지 모르겠다 ㅠ.ㅠ;

설마 standard_init_linux.go:219 이파일이 문제가 그럴리가

### 실행

```bash
$ docker-compose up
Creating network "docker-yona_default" with the default driver
Creating docker-yona_mariadb_1 ... done
Creating docker-yona_yona_1    ... done
Creating docker-yona_adminer_1 ... done
Attaching to docker-yona_mariadb_1, docker-yona_adminer_1, docker-yona_yona_1

...
더 이상의 자세한 설명은 생략한다.
...

Caused by: org.mariadb.jdbc.internal.util.dao.QueryException: Could not connect to address=(host=127.0.0.1)(port=3306)(type=master) : Connection refuse
```

위와 같은 DB 접속 오류 발생함

./yona/conf/application.conf 파일 131 라인을 보면 MariaDB 설정 부분이 있음

```yml
# MariaDB
db.default.driver=org.mariadb.jdbc.Driver
db.default.url="jdbc:mariadb://127.0.0.1:3306/yona?useServerPrepStmts=true"
db.default.user=yona
db.default.password=password
```

IP, PASSWORD 를 확인 해서 변경 해주자 다른 설정이 궁금하면 [참조](https://github.com/yona-projects/yona/blob/next/docs/ko/application-conf-desc.md) 해서 변경 하자
