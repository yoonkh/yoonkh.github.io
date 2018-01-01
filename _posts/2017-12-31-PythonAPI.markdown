---
layout: post
title:  "RESTful 파이썬 웹 제작"
date:   2017-12-31
author: Yoonkh
categories: Python
tags: 
- Python
- Django
- RESTfulAPI
comments: True
---

# RESTful 파이썬 웹 서비스 제작

## 장고를 이용한 레스트풀 API의 개발

### 간단한 SQLite 데이터 베이스와 대화하는 레스트풀 API 디자인

우리는 가장 적절한 **객체 관계형 매핑**을 선택하고 구성하는 데 시간을 낭비하고 싶지 않다. 가능한 한 빨리 레스트풀 API를 완성하고 모바일 앱을 통해 대화를 시작하길 원한다. 우리는 게임을 데이터베이스로 운영하길원하는데, 제작 준비가 필요하지 않으므로 복잡한 설치 또는 구성에 시간을 낭비하지 않고 가능하면 가장 단순한 관계형 데이터베이스를 사용할 수 있다. 

DRF라는 장고 레스트 프레임워크를 사용하면, 이 작업을 쉽게 완료해서 레스트풀 웹 서비스의 첫 번째 버전에 대한 HTTP 요청을 시작할 수 있다. 여기서는 새로운 장고 레스트 프레임 워크 프로젝트의 기본 데이터베이스인 매우 간단한 SQLite 데이터베이스로 작업할것이다. 

주요 자원에 대한 요구사항을 지정해야 한다. 다음 속성 또는 필드가 필요하다. 

- 정수 식별자
- 이름 또는 타이틀
- 출시일
- 3D RPG 또는 2D 모바일 아케이드와 같은 게임 카테고리 디스크립션
- 플레이어가 적어도 한 번 게임을 했는지 여부를 나타내는 bool 값

다음의 표는 첫 번째 API 버전에서 지원해야 하는 HTTP 동사, 범위, 그 메서드에 대한 의미를 보여준다. 

| **HTTP동사**  | **범위**  | **의미**  |
|---|---|---|
| GET  | 게임 컬렉션  | 컬렉션의 모든 저장도니 게임을 얻고, 이름에 따라 오름차순으로 정렬한다.  |
| GET  | 게임  | 게임 하나만 얻는다.  |
| POST  | 게임 컬렉션  | 컬렉션에 새 게임 생성  |
| PUT  | 게임  | 기존 게임 업데이트  |
| DELETE  | 게임  | 기존 게임 삭제  |

### 각 HTTP 메서드가 수행하는 작업 이해

새 게임을 만들려면 HTTP 동사(POST)와 요청 **URL**로 HTTP 요청을 작성해 보내야한다. 더욱이 **JSON** 키-값 쌍으로 필드 이름과 값을 제공해 새 게임을 만들어야 한다. 요청 결과, 서버는 필드에 제공된 값의 유효성을 검사하고 유효한 게임인지 확인한 후 데이터베이스에 저장한다.

서버는 적절한 테이블에 새 게임이 들어간 새 행을 삽입하고, JSON으로 직렬화된 최근 추가 게임의 JSON 본문과 201 Created 상태 코드를 반환하는데, 여기에는 데이터베이스가 자동으로 생성하고 게임 객체에 지정한 할당 id 또는 기본 키가 포함된다. 

```
POST http://localhost:8000/games/
```

id 또는 기본 키가 지정된 숫자 값과 일치하는 게임을 얻으려면 HTTP 동사(GET)와 요청 **URL**을 사용해서 HTTP 요청을 작성해 보내야 하는데, 여기서 {id}에는 id나 기본 키에 해당하는 숫자 값을 저장한다. 

```
GET http://localhost:8000/games/{id}/
```

id 또는 기본 키가 지정된 숫자 값과 일치하는 게임을 업데이트하려면 HTTP 동사(PUT)와 요청 **URL**을 사용해 HTTP 요청을 작성해 보내야 하는데, 여기서 {id} 자리에는 제공된 데이터로 생성된 게임의 해당 값으로 대체한다. 

```
PUT http://localhost:8000/games/{id}/
```

id 또는 기본 키가 지정된 숫자 값과 일치하는 게임을 제거하려면 HTTP 동사(DELETE)와 요청 **URL**을 사용해서 HTTP 요청을 작성해 보내야 하는데, 여기서 {id} 자리에 해당 숫자를 적는다. 

```
DELETE http://localhost:8000/games/{id}/
```

### 경량 가상 환경에서의 작업

먼저, 가상 환경을 위한 대상 폴더 또는 디렉터리를 선택해야 한다. 

```
~/PythonREST/Django
```

터미널을 열고, 다음 명령을 실행해 가상 환경을 만든다. 

```
python3 -m venv ~/PythonREST/Django01
```

맥 OS 또는 리눅스에서 bash 셸을 사용하게 터미널을 구성한 경우, 다음 명령을실행해 가상 환경을 활성화해야한다. 

```
source ~/PythonREST/Django01/bin/activate
```

가상환경이 활성화 되면 ```Yoon-MacBook-Pro:~ project$``` 에서 ```(Django) Yoon-MacBook-Pro:~ project$```으로 프롬프트가 변경된다.

### 장고 레스트 프레임워크에서의 가상 환경 설정

이제 다음의 명령을 실행해 장고 웹 프레임워크를 설치해야 한다.

```
pip install Django
```

장고 웹 프레임워크를 설치했으므로 장고 레스트 프레임워크를 설치할 수 있다. 

```
pip install djangorestframework
```

이제 다음 명령을 실행해 gamesapi라는 새 장고 프로젝트를 만든다. 

```
django-admin.py startproject gamesapi
```

그리고 나서 다음 명령을 실행해 gamesapi 장고 프로젝트 내에 games라는 새 장고 앱을 만든다. 

```
python manage.py startapp games
```

위의 명령으로 다음 파일들이 들어간 새 gamesapi/games 서브 폴더가 생성되었다. 

- ```__init__.py```
- ```admin.py```
- ```apps.py```
- ```models.py```
- ```tests.py```
- ```views.py```

```apps.py```파일의 파이썬 코드 ex)

```
From django.apps import AppConfig

Class GamesConfig(AppConfig):
	name='games'
```

이제 gamesapi/settings.py 파일을 열고 설치된 앱 선언의 문자열 리스트를 지정하는 행인 INSTALLED_APPS행을 찾아 다음의 내용을 추가한다. 

- 'rest_framework'
- 'games.app.GamesConfig'

### 모델 제작

```games/models.py``` 파일을 연다. 아래 행은 이 파일의 초기 코드를 보여주는데, 하나의 import문과 모델을 생성해야 함을 나타내는 주석이 있다. 

아래 행은 Game 클래스, 특히 ```games/models.py``` 파일에 있는 Game 모델을 만들기 위한 새 코드를 보여준다. 

```
From django.db import models 

Class Game(models.Model):
	Created = models.DateTimeField(auto_now_add=True)
	Name = models.CharField(max_length=200, blank=True, default='')
	release_date = models.DateTimeField()
	game_category = models.CharField(max_length=200, blank=True, default='')
	played = models.BooleanField(default=False)
	
	class Meta:
		ordering = ('name',)
```

다음으로는 새 Game 모델의 초기 마이그레이션을 만들어야 한다. 
장고는 SQLite 데이터베이스를 사용한다. 

```
python manage.py makemigrations games
```

이제 생성된 마이그레이션을 적용하기 위해 다음 파이썬 스크립트를 실행한다. 

```
python manage.py migrate
```

위의 명령을 실행하면 gamesapi 프로젝트의 루트 폴더에 db.sqlite3 파일이 생긴 것을 볼 수 있다. 장고가 생성한 테이블을 보려면 SQLite 명령 행 또는 SQLite 데이터베이스의 테이블을 쉽게 점검할 수 있게 해주는 애플리케이션을 사용하면 된다. 

다음의 명령을 실행해 생성된 테이블을 나열해 볼 수 있다. 

```
sqlite3 db.sqlite3 '.tables'
```

SQLite 데이터베이스 엔진과 데이터베이스 파일 이름은 ```gamesapi/settings.py``` 파이썬 파일에 지정돼 있다. 다음 행은 장고가 사용하는 모든 데이터베이스에 대한 설정을 담고 있는 DATABASE 딕셔너리의 선언을 보여준다. 

```
DATABASES = {
	'default': {
		'ENGINE': 'django.db.backends.sqlite3',
		'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
	}
}
```

마이그레이션을 실행한 후, SQLite 데이터베이스에는 다음 테이블이 생겼을 것이다. 

- auth_group
- auth_group_permissions
- auth_permission auth_user
- auth_user_groups
- auth_user_groups_permissions
- django_admin_log
- django_content_type
- django_migrations
- django_session
- games_game
- sqlitesequence

```games_game``` 테이블에는 SQLite 형식의 다음 행(필드라고도 함)이 있으며, 그 중 모두가 null 값도 가능한 것은 아니다. 

- id: The integer primary key, an autoincrement row
- created: datetime
- name: varchar(200)
- release_date: datetime
- game_category: varchar(200)
- played: bool

다음 행은 우리가 마이그레이션을 실행했을 때 장고가 생성한 SQL 생성 스크립트다. 

```
CREATE TABLE "games_game" {
	"id" integer NOT NULL PRIMARY KEY AUTOINCREMENT,
	"created" datetime NOT NULL,
	"name" varchar(200) NOT NULL,
	"release_date" datetime NOT NULL,
	"game_category" varchar(200) NOT NULL,
	"played" bool NOT NULL
}
```
