---
title: '[Docker] 도커에서 mariaDB 사용하기'
date: 2024-07-20 12:00:00 +0000
categories: [Docker, Mariadb]
tags: [Docker, Mariadb]
author: kaito
mermaid: true
---

> 본 게시물은 틀린 부분이 있을 수 있습니다, 참고용으로만 사용 부탁드립니다. 🥹
{: .prompt-warning }

## 개발환경
* M1 macbook
* Docker version 24.0.2

## 사용방법

![1_docker_pull](/assets/img/dev/2024-07-20/1_docker_pull.png)

```
docker pull mariadb
```

_docker hub에서 mariadb 이미지 pull_

---
<br>

![2_docker_run](/assets/img/dev/2024-07-20/2_docker_run.png)

```
docker run --name my-mariadb -e MARIADB_ROOT_PASSWORD=myPassword -p 3306:3306 -d mariadb
```

_`docker run` : Docker container를 실행_

_`--name my-mariadb` : container 이름을 "my-mariadb"로 부여_

_`-e MARIADB_ROOT_PASSWORD=myPassword` : Mariadb의 환경변수에 password를 할당하여 root user의 비밀번호를 변경_

_`-p 3306:3306` : 호스트(외부)의 3306포트를 내부의 3306포트로 매핑하여 외부에서 Docker mariadb를 사용 가능_

_`-d mariadb` : 컨테이너를 백그라운드 모드로 실행_

---
<br>

![3_docker_ps](/assets/img/dev/2024-07-20/3_docker_ps.png)

```
docker ps
```

_현재 실행 중인 Docker Container._

---
<br>

![4_docker_exec](/assets/img/dev/2024-07-20/4_docker_exec.png)

```
docker exec -it (mariadb_container_name) bash
```

_Mariadb Container 내부 Bash Shell에 접속_

---
<br>

![5_mariadb](/assets/img/dev/2024-07-20/5_mariadb.png)

```
mariadb -u root -p
```

_db 접속 시도 docker run에서 설정한 password로 접속_

---
<br>

![6_show_db](/assets/img/dev/2024-07-20/6_show_db.png)

_현재 모든 DB 목록을 표시_

_현재는 MariaDB 시스템에 관련된 DB만 있는 상태_

---
<br>

![7_create_db](/assets/img/dev/2024-07-20/7_create_db.png)

```
create database (DB_name);
```

_새로운 DB를 생성_

---
<br>

![8_use_db](/assets/img/dev/2024-07-20/8_use_db.png)

```
use (DB_name);
```

_해당 DB를 사용_

---
<br>

![9_create_table](/assets/img/dev/2024-07-20/9_create_table.png)

```
CREATE TABLE Account (
account_id INT AUTO_INCREMENT
PRIMARY KEY,
username VARCHAR(50) NOT NULL,
email VARCHAR(100) UNIQUE NOT NULL,
password VARCHAR(255) NOT NULL,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

_임의의 Account 테이블 생성_

---
<br>

![10_insert_db](/assets/img/dev/2024-07-20/10_insert_db.png)

```
INSERT INTO Account (username, email, password)
VALUES
('john_doe', 'john@example.com', 'password123'),
('jane_smith', 'jane@example.com', 'securepwd456'),
('bob_johnson', 'bob@example.com', 'strongpass789');
```

_Account 테이블에 임의의 데이터 삽입_

---
<br>

![11_select_db](/assets/img/dev/2024-07-20/11_select_db.png)

```
SELECT * FROM Account;
```

_삽입된 데이터 확인_
