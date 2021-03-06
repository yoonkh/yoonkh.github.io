---
layout: post
title:  "파이썬을 여행하는 히치하이커를 위한 안내서 - 웹 애플리케이션, 웹 배포, 웹 서버"
date:   2017-12-17
author: Yoonkh
categories: Python
tags:   
- Python
- Flask
comments: True
---

### 웹 애플리케이션 

파이썬은 빠른 프로토타이핑과 큰 프로젝트에 모두 적용되는 강력한 스크립팅 언어로써, 웹 애플리케이션 개발에 널리 사용된다. 

#### 웹 프레임워크/마이크로프레임워크

일반적으로 웹 프레임워크는 웹 애플리케이션 구현에 사용되는 라이브러리와 기본 핸들러 모음으로 구성된다. 대부분의 웹 프레임워크는 적어도 아래 나열된 내용을 수행하기 위한 패턴과 유틸리티를 포함한다. 

- URL 라우팅

	- 들어오는 HTTP 요청과 특정 파이썬 함수를 매칭한다. 

- 요청/응답 객체 처리 

	- 사용자의 브라우저에서 수신하거나 송신한 정보를 캡슐화한다.

- 템플릿

	- 파이썬 변수를 HTML 템플릿이나 기타 풀력에 삽입한다. 따라서 프로그래머가 레이아웃과 애플리케이션 로직을 구분할 수 있도록 돕는다. 

- 디버깅용 웹서비스 개발 

	- 작업 중인 머신에 소형 HTTP 서버를 실행해 빠르게 개발할 수 있다. 파일이 업데이트되면 서버 측 코드를 자동으로 재로딩한다. 

다음은 웹프레임워크에 대해서 다룬다.

#### 장고 

장고는 건전지가 포함된 웹 애플리케이션 프레임워크이며, 콘텐츠를 담는 웹사이트 제작에 적당한 훌륭한 선택지이다. 수많은 유틸리티와 패턴을 즉시 사용할 수 있어 복잡한 데이터베이스 기반 웹 애플리케이션을 빠르게 구축할 수 있으며 가독성 높은 코드 작성이 가능해진다. 

#### 플라스크

플라스크는 파이썬을 위한 마이크로프레임워크이며, 작은 애플리케이션, API, 웹 서비스를 구축할 때 훌륭한 선택지이다. 사용자가 원하는 대부분의 기능을 모두 제공하는 대신, URL 라우팅, HTTP 요청/응답 객체, 템플릿과 같이 웹 애플리케이션 프레임워크에서 주로 사용되는 핵심 구성 요소만 구현하였다. 플라스크를 사용한 앱 개발은 표준 파이썬 모듈을 작성하는것돠 같다. 

- 플라스크를 사용할 때 애플리케이션의 기타 구성 요소는 사용자가 스스로 선택한다. 예를 들어, 데이터베이스 접근, 양식, 생성/유효성 검증은 플라스크에 내장되어 있지 않다. 많은 웹 애플리케이션이 이러한 기능을 필요로 하지 않으므로 이는 훌륭한 점이다. 

#### 토네이도 

토네이도는 파이썬을 위한 비동기 웹프레임워크이며, 자체 이벤트 루프를 가진다. 이를 통해 웹 소켓 통신 프로토콜을 네이티브하게 지원할 수 있다. 토네이도는 다른 프레임워크와 달리 WSGI 애플리케이션이 아니다. 

#### 피라미드 

피라미드는 모듈성에 중점을 둔다는 점을 제외하면 장고와 매우 비슷하다. 더 적은 수의 내장 라이브러리가 포함되어 있으며, 스캐폴드라고 불리는 공유 가능한 템플릿을 통해 기본 기능을 확장하길 권장한다. 

### 웹 템플릿 엔진

대부분의 WSGI 애플리케이션은 HTTP 요청에 응답하고 HTTP이나 마크업 언어로 콘텐츨르 제공한다. 템플릿 엔진은 콘텐츠를 렌더링하는 데 사용된다. 불필요한 반복을 피하기 위해 계층/포함 체계를 사용해 템플릿 파일 모음을 관리하며, 템플릿의 정적 콘텐츠를 애플리케이션이 생성하는 동적 콘텐츠로 채운다. 

#### Jinja2	

새로운 파이썬 웹 애플리케이션에 적용할 템플릿 라이브러리로 Jinja2를 추천한다. Flask의 기본 엔진이며, 파이썬 문서를 만드는 도구인 스핑크스의 기본 엔진이기도 하다. 장고, 피라미드, 토네이도에 사용할 수도 있다. 텍스트 기반 템플릿 언어로 사용 할 수 있으므로 HTML 뿐만 아니라 마크업 언어를 생성하는 데 사용할 수도 있다. 

#### Chameleon

Chameleon은 HTML/XML 템플릿 엔진이며, Template Attribute Language, Expression Syntax, Macro Expansion TAL 구문을 사용해 구현되었다. Chameleon은 페이지 템플릿을 파싱하여 파이썬 바이트코드로 '컴파일'하여 로딩 속도를 높인다. 또한 피라미드에 사용된 기본 렌더링 엔진 중 하나다.

#### Mako 

Mako는 성능을 최대화하기 위해 파이썬으로 컴파일하는 템플릿 언어이며, Django와 Jinja2와 같은 다른 템플릿 언어에서 좋은 구문과 API를 가져왔다. 피라미드 웹 프레임워크의 기본 템플릿 언어이다.

- 다음은 Mako의 템플릿 예이다. 

```
<%inherit file="base.html"/>
<%
    rows = [[v for v in range(0,10)] for row in range(0,10)]
%>
<table>
    % for row in rows:
        ${makerow(row)}
    % endfor
</table>

<%def name="makerow(row)">
    <tr>
    % for name in row:
        <td>${name}</td>\
    % endfor
    </tr>
</%def>
```

- Jinja2와 같이 텍스트 마크업 언어이며, XML/HTML 문서 이외에도 사용될 수 있다. 

### 웹 배포 

#### 호스팅 

PaaS는 인프라 구조, 라우팅, 웹 애플리케이션 규모를 추상화하고 관리하는 클라우드 컴퓨팅 인프라의 일종이다. PaaS를 사용하는 개발자는 배포에 관한 사항이 아닌 애플리케이션 코드 작성에 집중 할 수 있게 된다. 

#### 헤로쿠

헤로쿠는 파이썬 웹 애플리케이션 배포에 추천하는 PaaS이다. 파이썬 2.7에서 3.5까지의 모든 애플리케이션을 지원한다. 헤로쿠 계정과 실제 데이터베이스/웹 서버 사이의 인터페이스를 위한 명령줄 도구 모음이 제공되므로, 웹 인터페이스를 사용하지 않고도 변경이 가능하다. 헤로쿠는 웹 개발자가 처음 애플리케이션을 개발할 때 필요한 단계별 지침뿐만 아니라, 파이썬을 헤로쿠와 함께 사용할 때 필요한 내용을 담은 글을 제공한다. 

#### 엘더리온

엘더리온은 Kubernetes, CoreOS, Docker를 기반으로 하는 PaaS이며, WSGI 애플리케이션을 지원한다. 

### 웹 서버 

Tornado를 제외한 모든 웹 애플리케이션 프레임워크는 WSGI 애플리케이션이다. 즉, HTTP요청을 받고 HTTP 응답을 보내기 위해 PEP 3333에 정의된 WSGI 서버와 상호작용을 해야한다. 

#### 엔진엑스

엔진엑스는 HTTP, SMTP와 같은 프로토콜용 웹 서버이자 역방향 프락시이다. 높은 성능, 상대적인 단순함, 여러 애플리케이션 서버와의 호환성으로 잘 알려져 있으며, 로드 밸런싱, 기본 인증, 스트리밍과 같이 편리한 기능이 포함되어 있다. 

#### 아파치 HTTP 서버 

아파치는 세계에서 가장 유명한 HTTP 서버 이지만, 파이썬 커뮤니티는 엔진엑스를 선호한다. 

#### WSGI 서버

독립형 WSGI 서버는 일반적으로 기존 웹 서버보다 적은 자원을 사용하고, 파이썬 WSGI 서버에 대한 벤치마크 실험에서 최고의 성능을 보여주었다. 이들은 엔진엔스나 아파치와 함께 역방향 프락시로 사용될 수 있다. 

다음은 가장 많이 사용되는 WSGI 서버이다 

- G유니콘

	- G유니콘은 새로운 파이썬 웹 애플리케이션에 권장되는 선택지로, 파이썬 애플리케이션을 제공하는 데 사용되는 순수 파이썬 WSGI 서버이다. 다른 파이썬 웹 서버와 달리, 사려 깊은 사용자 인터페이스가 있어 사용 및 구성이 매우 쉽다. 

- 웨이트리스 

	- 웨이트리스는 '아주 납득되는 성능'을 주장하는 순수 파이썬 WSGI 서버이다. 문서가 자세하지 않지만, G유니콘에는 없는 몇가지 좋은 기능을 제공한다. 그중 하나는 HTTP 요청 버퍼링인데, "Wait"-ress(기다림 없음)이라는 이름 그대로 느린 클라이언트가 응답하는 데 시간이 소요되더라도 차단하지 않는다. 

- uWSGI

	- uWSGI는 호스팅 서비스 구축에 사용되는 풀스택 서버다. 필요한 이유가 없다면 독립형 웹 라우터로 사용하지 않는게 좋다. uWSGI는 완전한 웹 서버 뒤에서 실행할 수 있다. 웹 서버는 uWSGI 프로토콜을 통해 uWSGI와 애플리케이션 작업을 구성할 수 있다. 
