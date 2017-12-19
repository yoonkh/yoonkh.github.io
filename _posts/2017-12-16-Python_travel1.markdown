---
layout: post
title:  "파이썬을 여행하는 히치하이커를 위한 안내서 - 훌륭한 코드 작성하기, 훌륭한 코드 읽어보기"
date:   2017-12-16
author: Yoonkh
categories: Python
tags:	
- Python
- Flask
comments: True
---

## 실전 돌입하기

### 훌륭한 코드 작성하기 

#### 코드 스타일 

- **PEP8**

	- PEP8은 파이썬을 위한 코드 스타일 가이드이며 작명 컨벤션, 코드 레이아웃, 공백, 그 외 유사 스타일 주제를 다룬다. 대체로 파이썬 코드를 작성할 때는 PEP8을 준수하는 것이 좋다. 코드 스타일이 통일되면 한 프로젝트 안에서 여러 개발자가 코드의 일관성을 유지하며 개발할 수 있는 밑거름이 된다. 

- **PEP 20(파이썬 계명)**

	- PEP20은 파이썬 코드를 작성할 때 겪는 의사 결정에 도움을 주는 원리 모음이다. 파이썬 셸에서 import this를 입력하면 전문을 볼 수 있다. 이름과는 달리 20개가 아닌 19개의 경구만 포함되어 있다(마지막 경구는 아직 작성되지 않았다)

- **일반적인 조언**

	- 파이썬 스타일 철학

		- "명시가 암시보다 좋다" 
		
			다음은 두 개의 값을 입력 받아 이들로 구성된 딕셔너리 형태의 결과를 출력하는 코드의 예다.

			나쁜예)
			
			```
			def make_dict(*args):
				x, y = args
				return dict(**locals())
			```
			
			좋은예)
			
			```
			def make_dict(x, y):
				return {'x': x, 'y':y}
			```
			
			좋은예의 코드에서는 함수에 x와 y가 명시적으로 입력되어 이들로 구성된 딕셔너리가 명시적으로 출력된다. 다른 개발자들이 함수 코드 첫 줄과 마지막 줄만 읽고도 무슨 함수인지 이해할 수 있도록 코드를 작성해야 한다. 나쁜예의 코드에서는 입력 값과 출력 값, 그리고 함수의 내용을 한눈에 이해하기 어렵다(물론, 함수가 두 줄뿐이라면 쉽긴 하다)
			
		- "여유로운 것이 밀집한 것보다 좋다" 

			한 줄에 하나의 구문만 작성하자. 간혹 리스트 컴프리헨션(list comprehension)과 같은 일부 복합 구문은 간결성과 표현성이 뛰어나기에 여러 개의 줄이 되어도 괜찮다. 그러나 서로 다른 구문은 여러 개의 줄로 구분하는 게 좋다. 이는 코드의 diff 결과의 가독성을 높이기도 한다. 
			
			나쁜예)
			
			```
			print('one'); print('two')
			
			if x == 1: print('one')
			
			if (<복잡한 표현 1> and
				 <복잡한 표현 >):
				 # 원하는 작업 수행 
		   ```
		   
		   좋은예)
		   
		   ```
		   print('one')
		   print('two')
		   
		   if x == 1:
		       print('one')
		       
	      cond1 = <복잡한 표현 1>
	      cond2 = <복잡한 표현 2>
	      if cond1 and cond2:
	      		# 원하는 작업 수행 
      	   ``` 
      	   
      	   파이써니스타들은 코드가 길어지더라도 한 줄에 한 구문씩 작성하고, 긴 조건무늘 여러 줄로 나누어 작성한다. 가독성을 위해서라면 파일 크기가 몇 바이트 증가하거나 계산 시간이 수 마이크로초 증가하는 것쯤은 기꺼이 감수한다. 
      	   
		- "오류 앞에서 절대 침묵하지 말지어다" 

			- 파이썬에서는 try문을 사용하여 오류를 처리한다. 다음의 내용은 벤자민 글라이츠만의 HowDoI 패키기 코드 중 일부이며, 오류 앞에서 침묵해도 되는 상황이 언제인지 알 수 있다.
			
				```
				def format_output(code, args):
						if not args['color']:
							return code
						lexer = None

						# 스택오버플로 태그에서 렉서를 찾거나
						# 쿼리 문자열로부터 렉서를 찾으려 시도
						for keyword in args['query'].split() + args['tags']:
							try:
								lexer = get_lexer_by_name(keyword)
								break
							except ClassNotFound:
								pass

						# 위에서 렉서를 찾지 못하면 렉서 추정 도구(guess_lexer)를 사용함
						if not lexer:
							lexer = guess_lexer(code)

						return highlight(code, lexer, TerminalFomatter(bg='dark'))
				``` 			
			
		- "함수 인자는 사용하기에 직관적이어야 한다"

			API 디자인에 따라 함수를 통해 소통하는 다운스트림 개발자의 경험이 달라진다. 인자는 다음과 같은 네 가지 방법으로 함수에 전달 될 수 있다.
			
			```
			def func(positional, keyword=value, *args, **kwargs):
				pass
			```
				
			1. 위치 인자(positional)은 필수이며 기본 값을 가지지 않는다.
			2. 키워드 인자(keyword=value)는 선택 사항이며 기본 값을 가진다.
			3. 가변 인자 리스트(*args)는 선택 사항이며 기본 값을 가진다. 
			4. 가변 키워드 인자 딕셔너리(**kwargs)는 선택 사항이며 기본 값을 가진다. 
	
		- "구현 결과를 설명하기 어렵다면, 그 아이디어는 나쁘다." 

			파이썬은 해커를 위한 강력한 도구이며, 어떠한 종류의 까다로운 작업도 가능하게 하는 후크와 도구를 풍부하게 보유하고 있다. 예를 들어 파이썬에서는 다음 작업이 가능하다. 
			
			- 객체를 생성하고 인스턴스화하는 방법을 변경
			- 파이썬 인터프리터가 모듈을 불러오는 방법을 변경
			- C 루틴을 파이썬에 임베딩

		- "우리는 모두 책임 있는 사용자다"

			파이썬에는 '프라이빗' 키워드가 없기 때문에 클라이언트 코드가 객체의 속성과 메서드를 덮어쓸 수 있다. 이는 자바와 같은 방어적 성격의 프로그래밍 언어와 매우 다른 철학을 보여준다. 자바에는 사용자가 안전한 방식으로 코드를 작성할 수 있도록 보호하는 장치가 내장되어 있지만, 파이썬은 그렇지 않다. 따라서 파이썬 사용자는 모두 책임감을 가져야 한다. 
			
		- "함수의 결과값은 한 곳에서만 반환하자"

			함수가 복잡할수록 반환문의 개수가 증가하기 쉽다. 그러나 의도를 명확히 하고 가독성을 유지하려면 의미 있는 결과 값을 최대한 적은 위치에서 반환하는 게 좋다. 함수 실행이 종료되는 경우는 두 가지다. 하나는 오류가 발생하여 종료되는 경우이고, 나머지 하나는 함수가 정상적으로 실행되어 결과 값을 반환한 뒤 종료되는 경우이다. 함수 실행 중 오류가 발생하면 None이나 False를 반환하는 것이 적절하다. 이 때 함수에서 오류와 관련된 문맥이 파악되자마자 결과 값을 반환하도록 하여 함수 구조를 수평적으로 만드는 것이 좋다. 만약 오류가 발생하지 않는다면, 그 다음 코드가 실행되기 위한 조건이 충족된 것이며, 함수 실행이 멈추지 않고 지속된다. 가끔은 여러 개의 반환문을 사용하는 것도 필요하다. 

- **컨벤션**

	- 컨벤션은 모두에게 수긍이 가는 방식이지만 유일한 선택지는 아니다. 컨벤션은 일반적으로 널리 사용되며, 코드의 가독성을 높이는 데 도움이 된다.

		- 같음을 확인하기 위한 대안

			나쁜예)
			
			```
			if attr == True:
			print 'True!'
			
			if attr == None:
			print 'attr is None!'
			```
			
			좋은예)
			
			```
			# 값이 존재하는지 확인
			if attr:
				print 'attr is truthy!'
				
			# 값이 존재하지 않는지 확인
			if not attr:
				print 'attr is falsey!'
				
			# 값이 'True'인지 확인
			if attr is True:
				print 'attr is True'
				
			# 값이 'None'인지 확인
			if attr is None:
				print 'attr is None!'
			```
			
		- 딕셔너리 요소에 접근하기 

			dict.has_key 메서드 대신 x in d 구문을 사용하거나 dict.get()에 기본 인자를 전달하자.
			
			나쁜예)
			
			```
			>>> d = {'hello': 'world'}
			>>>
			>>> if d.has_key('hello'):
			... 	print(d['hello']) # 'world' 출력
			... else:
			... 	print('default_value')
			world
			```
			
			좋은예)
			
			```
			>>> d = {'hello': 'world}
			>>> 
			>>> print (d.get('hello', 'default_value')
			world
			>>> print (d.get('howdy', 'default_value')
			default_value
			>>>
			>>> # 아니면,
			... if 'hello' in d:
			... 	print(d['hello'])
			...
			world
			```
			
		- 리스트 다루기

			리스트 컴프리헨션은 리스트 자료형을 다루는 명확하고 강력한 도구다!
			
			일반 반복문)
			
			```
			# 4보다 큰 성분만 남기기
			a = [3, 4, 5]
			b = []
			for i in a:
				if i > 4:
					b.append(a)
					
			# 모든 리스트 성분에 3씩 더하기
			a = [3, 4, 5]
			for i in range(len(a)):
				a[i] += 3
			```
			
			리스트 컴프리헨션)
			
			```
			# 리스트 컴프리헨션이 좀 더 깔끔하다
			a = [3, 4, 5]
			b = [i for i in a if i > 4]
			
			# 아니면 다음과 같이 사용해보자
			b = filter(lambda x: x > 4, a)
			
			# 여기도 마찬가지로 깔끔하다
			a = [3, 4, 5]
			a = [i + 3 for i in a]
			
			# 람다 표현식을 사용할 수도 있다
			a = map(lambda i: i + 3, a)
			```
			
### 프로젝트 구조화하기

#### 데코레이터 

데코레이터는 파이썬 2.4에서부터 추가되었다. 데코레이터는 다른 함수나 메서드를 감싸는 (혹은 장식하는) 함수 혹은 클래스 메서드이다. 장식에 사용된 함수나 메서드는 원래의 함수나 메서드를 바꾼다. 

```
>>> def foo():
... 	print("I am inside foo.")
...
...
...
>>> import logging
>>> logging.basicConfig()
>>> 
>>> def logged(func, *args, **kwargs):
... 	logger = logging.getLogger()
... 	def new_func(*args, **kwargs):
... 		logger.debug("calling {} with args {} and kwargs {}".format(
... 						func.__name__, args, kwargs))
... 		return func9*args, **kwargs)
... 	return new_func
...
>>>
... @logged
... def bar():
... 	print("I am insdie bar.")
...
>>> logging.getLogger().setLevel(logging.DEBUG)
>>> bar()
DEBUG:root:calling bar with args () and kwargs {}
I am inside bar.
>>> foo()
I am inside foo.
```

- 이 메커니즘은 함수나 메서드의 핵심 논리를 유지하는 데 유용하다. 

#### 동적 타이핑

파이썬은 변수의 타입이 고정되지 않은 동적 타입(dynamically typed)언어다. 파이썬에서는 동적 타이핑이 약점으로 여겨지기도 한다. 디버깅하기 어려운 복잡한 코드를 야기하는 경우가 있기 때문이다. 만약 a라는 변수가 다양한 무언가에 할당된다면, 개발자나 관리자는 변수가 가리키는 대상이 서로 완전히 무관한지 확인하기 위해 코드에서 a가 등장하는 모든 부분을 추적해야 한다.  

#### 변경 가능/불가능한 자료형

파이썬의 자료형은 내장 자료형과 사용자 정의 자료형으로 나뉜다. 

```
# 리스트는 변경 가능 
my_list = [1, 2, 3]
my_list[0] = 4
print(my_list) # [4, 2, 3] <- 같은 리스트이며, 변경사항이 적용됨

# 정수는 변경 불가능
x=6
x = x + 1 # 메모리의 다른 위치에 새 x가 만들어짐
```

- 변경 가능한 자료형 

	- 객체 내용에 대한 제자리 연산이 가능핟. 리스트와 딕셔너리가 그 예시이며, list.append()나 dict.pop()과 같은 메서드를 사용하면 제자리에서 값이 변경된다. 

- 변경 불가능한 자료형

	- 객체 내용을 바꾸는 메서드를 제공하지 않는다. 예를 들어, 변수 x에 정수 6이 할당되어 있다면, 'increment'메서드를 사용할 수 없다. 그래서 x + 1을 계산하려면 새 정수를 만들어 이름을 정해줘야 한다. 

변경 가능 여부에 따른 결과 중 하나는 변경 가능한 자료형을 딕셔너리 키로 사용할 수 없다는 것이다. 딕셔너리는 키 저장을 위해서 해싱(hashing)을 사용하는데, 값이 변경된다면 같은 값에 해시될 수 없기 때문에 해싱을 사용할 수 없다. 변경 불가능한 자료형 중 리스트 대신 사용할 수 있는 것은 튜플이다. 튜플은 소괄호로 만들 수 있는데, 제자리에서 값을 변경할 수 없기 때문에 딕셔너리 키로 사용할 수 있다. 

#### 의존성 벤더화

**의존성을 벤더화**한 패키지는 외부 의존성(서드파티 라이브러리)을 소스 코드에 포함하고 있다. 이 소스 코드는 *vendor*나 *packages*라는 폴더 안에 들어있다. 대부분의 경우에는 의존성을 별도로 분리하는 게 좋다는 것이 중론이다. 그렇지 않으면 코드 저장소에 불필요한 내용(종종 메가 바이트의 추가 코드)이 늘어나기 때문이다. 

- 만약 커다란 변경사항에 대한 풀리퀘스트(Pull request)를 제출하면, 다른 사용자의 추가 제안이나 요청을 수렴하여 유지 관리를 해야 할 수도 있다는 것이다. 이러한 이유로 Tablib과 Requests는 일부 의존성을 벤더화하였다.


### 코드 테스트 

코드 테스트는 매우 중요하다. 프로젝트가 잘 작동하지 않으면 사람들이 사용하지 않을 것이다. 2001년에 발표된 파이썬 2.1부터는 doctest와 unittest를 포함하였고, 테스트 주도 개발(Test-development, TDD)을 채택하였다. TDD란 함수를 구현하기 이전에 함수의 주 연산과 예외 사례를 정의한 테스트 케이스를 작성하고, 이를 통과하도록 함수 코드를 작성하는 방식이다. 이후로 TDD는 비즈니스 및 오픈소스 프로젝트에 널리받아들여지고 채택되었다. 

#### 테스트를 위한 팁

테스트는 히치하이커가 작성할 수 있는 가장 유용한 코드일 것이다. 

#### 한번에 하나씩 테스트 

기능은 작은 단위에 초점을 맞춰 테스트해야 해당 기능이 제대로 작동하는지 증멸할 수 있다. 

#### 독립은 필수

각 테스트 유닛은 서로 독립적이어야 한다. 각자 실행 가능해야 하고, 테스트 슈트로도 실행 가능해야 하며, 호출 순서에 관계없이 한꺼번에 실행이 가능해야 한다. 

#### 함수 이름은 길고 정확하게

테스트 함수 이름에 테스트 내용이 포함되도록 긴 이름을 사용하자! 이는 코드 실행에서 짧은 이름이 선호되는 것과는 조금 다른 지침인데, 테스트 함수가 명시적으로 호출되는 일이 없기 때문이다. 

#### 속도가 중요하다!

한 번의 테스트가 실행될 때 수 밀리 초 이상이 소요되면 개발 속도가 느려지거나, 테스트가 원하는 만큼 자주 실행되지 않는다. 경우에 따라 복잡한 데이터 구조 때문에 테스트마다 데이터 구조를 로딩하느라 느려지기도 한다. 

#### 메뉴얼을 읽자!

사용하는 도구가 개별 테스트나 테스트 케이스를 어떻게 수행하는지 익혀야 한다. 모듈 내 함수를 개발할 때는 함수 테스트를 자주 해야 하고, 가능하다면 코드가 저장될 때마다 자동으로 수행해야 한다. 

#### 코딩 시작 전과 후에 모든 테스트를 수행하자

코딩 시작 전에 테스트 슈트 전체를 돌리고, 코딩이 끝나고 다시 한 번 돌려야 한다. 그래야 코드 작성 부분 이외의 나머지 부분이 깨지지 않았다고 확신할 수 있다. 

#### 버전 관리 자동화 후크는 매혹적이다

공유 저장소에 코드를 보내기 전에는 모든 테스트를 수행하는 후크를 구현하는 것이 좋다. 

#### 쉬고 싶을 때는 고장 난 테스트를 작성하자

개발 도중 작업을 멈춰야 할 때, 그다음 개발해야 할 부분에 고장 난 단위 테스트를 작성하는 것이 좋다. 다시 작업하러 돌아왔을 때 해당 지점에서부터 다시 시작할 수 있으며 기존 작업을 빠르게 파악할 수 있다. 

#### 테스트를 사용하여 디버깅하자

디버깅의 시작은 버그를 찾아내는 테스트를 작성하는 것이다. 매번 테스트를 작성하는 게 번거로울 수도 있다. 그러나 버그를 찾아내는 테스트 코드는 여러분의 프로젝트 코드 중 가장 가치 있는 부분 중 하나일 것이다. 

#### 공동 작업자가 이해하기 쉬운 테스트를 작성하자

무언가 잘못됐거나 고쳐야 할 때 코드에 좋은 테스트 모음이 있다면, 여러분이나 다른 유지 관리자가 문제를 수정하거나 특정 동작을 수정하기 위해 테스트 슈트에 전적으로 의지할 것이다. 따라서 테스트 코드를 실행 코드와 비슷한 수준 혹은 그 이상으로 많이 읽게 될 것이다. 이때 의도가 불분명한 단위 테스트는 별 도움이 되지 않는다. 

#### 설명하기 쉬운 테스트가 좋다

테스트 코드는 새로 합류한 개발자들을 위한 안내의 용도로 사용된다. 새로 합류한 개발자가 이미 만들어진 코드에서 작업해야 할 때는 테스트 코드를 돌려보고 읽어보는 게 최선의 방법일 때가 많다. 그렇게 하면, 코드 중 문제가 있는 부분이나 예외가 발생하는 부분이 어디인지 발견할 수 있다. 

#### 무엇보다, 혼란에 빠지지 말자

오픈 소스의 세계에서 여러분은 혼자가 아니다!!

#### 테스트를 위한 기본

#### unittest

unittest는 건전지(프로그래머가 바로 사용할 수 있는 라이브러리와 통합 환경을 제공한다는 파이썬의 기본 개념)가 포함된 테스트 모듈로, 파이썬 표준 라이브러리에 포함되어 있다. 

```
# test_example.py
import unittest

def fun(x):
	return x + 1
	
class MyTest(unittest.TestCase):
	def test_that_fun_adds_one(self):
		self.assertEqual(fun(3),4)
		
class MySecondTest(unittest.TestCase):
	def test_that_fun_fails_when_not_adding_number(self):
		self.assertRaises(TypeError, fun, "multiply six by nine")
```

#### Mock(unittest.mock)

파이썬 3.3부터 unittest.mock이 표준 라이브러리에서 제공된다. mock을 사용하면 테스트중인 시스템의 일부를 mock 객체로 바꿔 어떻게 사용되고 있는지 알 수 있다. 

```
from unittest.mock import MegicMock

instance = ProductionClass()
instance.method = MagicMock(return_value=3)
instance.method(3, 4, 5, key='value')

instance.method.assert_called_with(3, 4, 5, key='value')
```

- 테스트 중인 모듈에서 mock 클래스나 mock 객체를 만들고 싶다면, patch 데코레이터를 사용하자!

#### doctest

docktest 모듈은 문서화 문자열 안에 대화형 파이썬 세션처럼 보이는 텍스트가 있는지 검사하고, 해당 세션을 실행하여 쓰여진 대로 정확히 동작하는지 확인한다. 

```
def square(x):
	"""x를 제곱함.
	
	>>> square(2)
	4
	>>> square(-2)
	4
	"""
	
	return x * x
	
if __name__ == '__main__':
	import doctest
	doctest.testmod()
```

- 명령줄에서 해당 모듈을 실행하면(예: python module.py) doctest가 작동하면서, 문서화 문자열에 기술된 대로 동작하지 않으면 경고한다. 

#### 예시 

테스트 슈트를 실행하려면 패키지에 포함되지 않은 별도의 라이브러리가 필요하다(예: Requests에서는 모의 HTTP 서버를 구축하기 위해 Flask패키지를 사용함). 해당 라이브러리는 ```requirements.txt```에 명시되어 있다.

**예시: Tablib에서의 테스트**

Tablib는 테스트를 위해 파이썬 표준 라이브러리의 unittest 모듈을 사용한다. 

```
#!/usr/bin/env python
# -*- coding: utf-8 -*-
"""Tests for Tablib."""

import json
import unittest
import sys
import os
import tablib
from tablib.compat import markup, unicode, is_py3
from tablib.core import Row




class TablibTestCase(unittest.TestCase): # 1번
    """Tablib test cases."""

    def setUp(self): # 2번
        """Create simple data set with headers."""

        global data, book

        data = tablib.Dataset()
        book = tablib.Databook()

        #
        # ... 여기서 사용하지 않는 구성 생략 ...
        #

    def tearDown(self): # 3번
        """Teardown."""
        pass


    def test_empty_append(self): # 4번 
        """Verify append() correctly adds tuple with no headers."""
        new_row = (1, 2, 3)
        data.append(new_row)

        # Verify width/data
        self.assertTrue(data.width == len(new_row))
        self.assertTrue(data[0] == new_row)


    def test_empty_append_with_headers(self): # 5번
        """Verify append() correctly detects mismatch of number of
        headers and data.
        """
        data.headers = ['first', 'second']
        new_row = (1, 2, 3, 4)

        self.assertRaises(tablib.InvalidDimensions, data.append, new_row)
```	

- 1번: unittest를 사용하기 위해서는 unittest.TestCase를 상속받는 서브 클래스를 만들고, test로 시작하는 이름의 테스트 메서드를 작성한다. TestCase는 단정 메서드를 제공하며, 같음, 참거짓, 데이터 타입, 집합 포함 여부, 예외 발생 여부 등을 확인한다

- 2번: TestCase.setUp()은 TestCase의 매 테스트 메서드가 실행되기 전에 실행된다. 

- 3번: TestCase.tearDown()은 TestCase의 매 테스트 메서드가 실행되고 난 후에 실행된다. 

- 4번: 모든 테스트 메서드의 이름은 test로 시작해야 하며, 그렇지 않으면 실행되지 않는다. 

- 5번: 하나의 TestCase 안에 여러 개의 테스트가 있을 수 있으나, 각각 하나의 내용만 테스트 해야 한다. 

### 그 외 인기 있는 도구들

#### pytest

pytest는 파이썬 표준인 unittest 모듈에 대한 비표준 대안이다. 즉, 테스트 클래스의 스캐폴딩이 필요 없으며, setup이나 teardown 메서드 또한 필요하지 않을 수 있다. 

#### Nose

Nose는 테스트를 보다 쉽게 할 수 있도록 unittest를 확장한 것이다. Nose는 자동으로 테스트를 발견하며, 수작업으로 테스트 슈트를 만드는 수고를 덜어준다. 

#### tox

tox는 테스트 환경 관리를 자동화하고, 다중 인터프리터 구성에서 테스트하기 위한 도구다.

#### Lettuce 와 Behave 

Lettuce와 Behave는 파이썬 행동 주도 개발(Behavior-driven development, 이하 BDD)을 위한 패키지이다. BDD는 2000년대 초 테스트 주도 개발(TDD)에서 파생한 개발 프로세스이며, TDD에서 '테스트'란 단어를 '행동'으로 대체하여 초보자가 TDD를 어려워하는 문제를 극복하고자 하였다. 

### 문서 

파이썬 개발자에게는 프로젝트의 가독성 뿐만 아니라 문서 가독성도 중요하다. 

#### 프로젝트 문서

프로젝트 문서에는 프로젝트 사용자를 위한 API 문서가 있고, 기여자를 위한 별도의 문서가 있다. 여기서는 후자를 다룬다. 최상위 디렉터리의 README 파일은 프로젝트 사용자와 관리자 모두에게 필요한 정보를 제공하며, 텍스트 또는 마크업 언어로 작성해야 한다. 마크업 언어로는 reStructuredText나 마크다운이 있다. 프로젝트나 라이브러리의 목적을 (사용자가 아무것도 모른다고 가정하고) 설명해야 하며, 소프트웨어의 주요 소스 URL과 기본 크레딧 정보가 포함되어야 한다. README 파일은 코드 독자에게 주요 시작점이 된다. 

#### 프로젝트 공개 

문서에는 프로젝트에 따라 아래 구성 요소 전부 혹은 일부가 포함될 수 있다. 

- 소개(introduction)에서는 프로젝트 기능을 한두 개 정도의 매우 간단한 용례로 소개해야 한다. 30초 가량의 프로젝트 홍보라고 생각하자!

- 튜토리얼(tutorial)에서는 주요 용례를 보다 자세히 설명해야 한다. 독자가 프로토타입을 구성할 수 있을 정도로 단계별로 설명하자!

- API 레퍼런스(API reference)는 코드로부터 만들어지는 게 전형적이며, 공개적으로 사용 가능한 인터페이스, 파라미터, 반환 값을 나열한다.  

- 개발자 문서(Developer documentation)는 미래의 기여자를 위해 작성되며, 코드 컨벤션이나 프로젝트의 일반 디자인 전략이 포함될 수 있다. 

#### 스핑크스 

Sphinx는 가장 널리 사용되는 파이썬 문서화 도구다. reStructuredText 마크업 언어를 HTML, LaTex(출력 가능한 PDF 버전용), 메뉴얼 페이지 그리고 일반 텍스트와 같은 다양한 형식으로 변환한다. 

### 로그

대체로 로그를 남기는 데에는 두 가지 목적이 있다. 

- 진단용 로그

진단용 로그는 애플리케이션 작동에 관한 이벤트 기록이다. 예를 들어, 사용자가 오류 보고서를 남기면 로그에서 해당 오류의 문맥을 파악할 수 있다. 

- 감시용 로그

감시용 로그는 비즈니스 분석에 사용되는 이벤트 기록이다. 사용자의 거래를 추출하여 다른 세부 정보와 결합하여 보고서를 작성하거나 업무를 최적화 할 수 있다. 

#### 라이브러리에서 로그 남기기

**"NullHandler 이외의 핸들러는 라이브러리의 로그 기록기에 추가하지 않는 게 좋다!"**

로그 기록 이벤트가 발생했을 때 무슨 일인지 알아내는 주체는 라이브러리가 아닌 사용자다. 따라서 위의 경고는 아무리 반복해도 지나치지 않는다. Nullhandler는 이름 그대로 아무것도 하지 않으며 사용자가 원하지 않는 경우에 로그 기록을 명시적으로 해제해야 한다. 

#### 애플리케이션에서 로그 남기기

| **방법**  | **장점**  | **단점**  |
|---|---|---|
| INI 형식의 파일 사용  | logging.config.listen()함수를 사용하면, 코드 실행 도중에도 구성을 업데이트하고 소켓의 변경사항을 가져올 수 있다.  | 코드에서 로그를 구성하는 것보다 제어력이 낮다  |
| 딕셔너리나 JSON 형식 파일 사용  | 실행 중 업데이트할 수 있을 뿐만 아니라, json 모듈을 사용해 파일로부터 구성을 불러올 수도 있다.  | 코드에서 로그를 구성하는 것보다 제어력이 낮다.  |
| 코드 사용  | 모든 구성을 완벽히 제어할 수 있다.  | 구성을 수정하려면 소스 코드를 변경해야 한다.  |

### 라이선스 선택 

미국에서는 소스 코드를 배포할 때 라이선스를 명시하지 않으면, 법적으로 사용자는 이를 다운로드/수정/배포하지 못한다. 또한 사람들에게 규칙을 알려주지 않으면 아무것도 프로젝트에 기여하지 못한다. 따라서 라이선스가 필요하다.

#### 업스트림 라이선스

다른 프로젝트에서 파생된 결과물이라면 업스트림(upstream) 라이선스에 따라 라이선스가 정해진다. 예를 들어, 파이썬 소프트웨어 재단에서는 파이썬 소스 코드에 기여한 모든 참여자에게 해당 코드가 파이썬 소프트웨어 재단에 공식적으로 귀속된다는 내용(본인의 저작권은 유지됨)의 동의 서명을 요청한다. 참고로 기여자는 두 가지 라이선스 중 선택할 수 있다. 

#### 선택사항

선택할 수 있는 라이선스는 무수히 많지만, 파이썬 소프트웨어 재단에서는 OSI(Open Source Institute)에서 승인한 라이선스 중에서 고르길 추천한다. 

*오픈 소스 라이선스는 대체로 다음의 두 카테고리 중 하나에 속한다*

- 허용 라이선스

허용 라이선스(permissice license)는 종종 BSD(Berkeley Software Distri-bution, 버클리 소프트웨어 배포) 스타일 라이선스로 불리며, 사용자가 자유롭게 원하는 대로 소프트웨어를 사용하는 데에 초점을 둔다. 

- 카피 레프트 라이선스

카피레프트(copyleft) 라이선스는 덜 허용적인 라이선스라고도 불리며, 소스 코드가 그 자체로 사용 가능하도록 하는 데 중점을 둔다. GPL 라이선스가 가장 잘 알려져 있다.
			
## 훌륭한 코드 읽어 보기 

프로그래머는 수많은 코드를 읽어야 한다. 능수능란한 프로그래머가 되는 비결은 탁월한 코드를 읽고, 이해하고, 따라잡는 데 있다. 

### HowDoi

벤자민 글라이츠만의 HowDoI 프로젝트는 코드 전체가 300줄이 채 안되며, 이번 코드 읽기 여정을 시작하기에 제격이다. 

#### 단일 파일 스크립트 읽기

스크립트는 대체로 명료한 시작점, 명료한 옵션, 명료한 종료점이 있으며, API나 프레임워크를 제공하는 라이브러리보다 이해하기 쉽다. 

#### HowDoI의 문서 읽기

HowDoI는 프로그래밍에 관한 질문의 답을 인터넷에서 찾도록 돕는 조그마한 명령줄 애플리케이션이다!

```
usage: howdoi.py [-h] [-p POS] [-a] [-l] [-c] [-n NUM_ANSWERS] [-C] [-v] QUERY [QUERY ...]

instant coding answers via the command line

positional arguments:
  QUERY                 the question to answer

optional arguments:
  -h, --help            show this help message and exit
  -p POS, --pos POS     select answer in specified position (default: 1)
  -a, --all             display the full text of the answer
  -l, --link            display only the answer link
  -c, --color           enable colorized output
  -n NUM_ANSWERS, --num-answers NUM_ANSWERS
                        number of answers to return
  -C, --clear-cache     clear the cache
  -v, --version         displays the current version of howdoi
```

#### HowDoI 사용하기

```
(venv)$ howdoi --num-answers 2 python lambda function list comprehension
--- Answer 1 ---
[(lambda x: x*x)(x) for x in range(10)]

--- Answer 2 ---
[x() for x in [lambda m=m: m for m in [1,2,3]]]
# [1, 2, 3]
```

#### HowDoI의 코드 읽기

howdoi.py를 훑어보면 각 함수가 그 다음 함수에서 사용되는 것을 알 수 있어 흐름을 이해하기 쉽다. 또한 함수 이름만 봐도 알 수 있듯이, 함수별로 단 하나의 작업이 주어져 있다. 메인 함수인 ```command_line_runner()```는 howdoi.py 파일의 마지막 부분에 있다. 

#### HowDoI의 구조 예시

HowDoI는 작은 라이브러리이기 때문에 구조에 대해 짚고 넘어갈 점이 별로 없다 

#### 하나의 함수는 하나의 일만 하도록 하자!

HowDoI의 함수는 각자 하나의 일만 처리하도록 분리되어 있다. 이게 얼마나 유익한지는 아무리 강조해도 모자르다. 심지어 다른 함수의 try/except문을 위해서만 존재하는 함수도 있다(```_format_output()```는 예외인데, try/except를 통해 예외처릴르 하는게 아니라, 구문 강조에 사용할 코딩 언어를 식별한다!)

#### 시스템에서 사용할 수 있는 데이터 활용

HowDoI는 관련 시스템 값을 확인하고 사용한다. 프락시 서버를 처리하기 위한 ```urllib.request.getproxies()```가 하나의 예다!(학교와 같은 기관에서 중간 서버를 통해 인터넷 연결 중 일부를 제한하는 경우)

#### HowDoI의 스타일 예시

HowDoI는 대체로 PEP8을 따르지만, 가독성이 떨어진다면 따르지 않는다. 예를 들어, import문은 파일의 맨 위에 위치하지만 표준 라이브러리와 외부 모듈이 뒤섞여 있다. 

#### 밑줄이 앞에 붙은 함수 이름(우리는 모두 책임 있는 사용자다)

HowDoI의 거의 모든 함수명 앞에 밑줄이 붙어 있다. 이는 패키지의 내부에서만 사용되는 함수임을 의미한다. 

#### 호환성은 한 곳에서만 처리(가독성은 중요하다)

메인 코드가 실행되기 전에 의존성 버전 차이를 처리한다. 이는 코드 독자에게 의존성 문제가 없을 거란 확신을 주고, 버전 확인 코드가 도처에 남용되지 않도록 막는다. 이 점은 HowDoI가 명령줄 도구이므로 장점이다. 명령줄 도구를 사용하려고 파이썬 인터프리터 버전을 바꾸려는 사람은 거의 없을 것이기 때문이다.

#### 파이썬스러운 선택(아름다움이 추함보다 좋다)

아래 스니펫은 howdoi.py에서 가져왔으며, 파이썬스럽고 사려 깊은 선택이 뭔지 보여 준다. ```get_link_at_pos()``` 함수는 결과가 없으면 False를 반환하고, 아니면 결과 링크 중 스택오버플로 링크를 판별하여 적절한 위치의 링크(링크가 충분하지 않으면 마지막 위치의 링크)를 반환한다.

```
def _is_question(link): # 1번
	return re.search('questions/\d+/', link)
	
# [ ... 기타 함수 생략 ... ]

def get_link_at_pos(links, position):
    links = [link for link in links if _is_question(link)] # 2번   
    if not links:
        return False # 3번

    if len(links) >= position:
        link = links[position - 1] # 4번
    else:
        link = links[-1] # 5번
    return link # 6번
```

- 1번: ```_is_question()```은 한 줄짜리 함수이며, 불명확한 정규 표현식 검색에 명확한 의미를 부여한다. 

- 2번: 리스트 컴프리헨션이 문장처럼 읽힌다. 이는 ```_is_question()```을 따로 분리해 정의하고, 의미 있는 변수명을 사용한 덕분이다. 

- 3번: 이른 반환문은 보다 수평적인 구조의 코드를 만들어준다. 

- 4번: link 변수에 값을 지정해주는 추가 단계다. 

- 5번: 여기에선 새로운 변수 선언 없이 두 개의 서로 다른 return문을 사용하는 대신, 명확한 변수명의 link를 사용하여 ```get_link_at_pos()```의 목적을 확실하게 드러냈다. 그 결과 코드 자체가 문서처럼 쉽게 읽힌다. 

- 6번: 최상위 들여쓰기 수준에 위치한 하나의 반환문은 각종 코드 경로가 이곳에서 종료됨을 명시적으로 보여준다. 코드의 첫 줄과 마지막 줄만 읽으면 함수가 무슨 일을 하는지 알 수 있다는 단순한 규칙이 여기에도 적용된다.

### Diamond 

Diamond는 시스템 수치를 수집하여 다운스트림 프로그램에 전달하는 데몬(백그라운드 프로세스 상태로 계속 실행되는 애플리케이션)이다. 다운스트림 프로그램으로는 MySQL, Graphite 등이 있다. 

#### 보다 큰 애플리케이션 코드 읽기

Diamond는 HowDoI와 같은 명령줄 애플리케이션이다. 코드 파일이 여러 개임에도 여전히 시작점과 실행 경로가 명료하다. 

#### Diamond 사용하기 

먼저 Diamond/tmp 폴더를 만들어 수정된 구성 파일을 해당 위치로 옮긴다. 

폴더 생성은 Diamond 폴더에서 다음과 같이 입력하면 된다.

```
(venv)$ mkdir tmp
(venv)$ cp conf/diamond.conf.example tmp/diamond.conf
```

그리고 tmp/diamond.conf 파일을 다음과 같이 수정한다.

```
### Options for the server
[server]
# Handlers for published metrics. # 1번 
handlers = diamond.handler.archive.ArchiveHandler
user = # 2번
group = 
# Diarectory to load collector modules from # 3번
collectors_path = src/collectors/

### Options for handlers # 4번
[handlers]
[[default]]

[[ArchiveHandler]]
log_file = /dev/stdout

### Optrions for collectors
[collectors]
[[default]]
# Default Poll Interval (seconds)
interval = 20 

#### Default enabled collectors
[[CPUCollector]]
enabled = True

[[MemoryCollector]]
enabled = True
```

- 1번: 여러 핸들러가 있고, 클래스 이름을 사용해 선택할 수 있다. 

- 2번: 데몬을 실행할 사용자와 그룹을 제어할 수 있다.

- 3번: 콜렉터 모듈을 찾을 경로를 지정할 수 있다. 구성 파일에 경로를 명시하지 않으면 Diamond는 사용자가 만든 Collector 서브 클래스를 찾지 못한다. 

- 4번: 구성 핸들러를 개별로 저장할 수 있다. 

#### Diamond 코드 읽기

큰 프로젝트의 코드를 읽을 때는 IDE가 유용하다. 소스 코드에서 함수와 클래스가 정의된 위치를 빠르게 찾을 수 있고, 주어진 정의가 사용된 모든 위치를 찾을 수도 있다. 이러한 기능을 사용하기 위해 가상환경의 파이썬 인터프리터를 IDE의 인터프리터로 지정해주자!

diamond는 util로부터 버전 정보를 얻고, utils.log를 사용해 로그 기록 설정을 하고, server를 통해 서버를 가동한다. server는 util 패키지의 거의 모든 모듈을 불러온다. utils.classes를 통해 handler.Handler와 collector에 접근하고, utils.config를 통해 구성 파일에서 콜렉터 설정을 불러온다. 그리고 utils.schedular를 통해 콜렉터가 수치를 계산하기 위한 폴링 간격을 설정하고, utils.signals을 통해 핸들러를 구성하고 시작한다!

#### Diamond의 구조 예시 

Diamond는 실행 가능한 애플리케이션이면서 맞춤형 콜렉터를 만들고 사용할 수 있는 방법을 제공하는 라이브러리이기도 하다.

#### 서로 다른 기능을 네임스페이스로 분리하자(네임스페이스는 대박 좋은 아이디어였다!)

server 모듈이 diamond.handler, diamond.collector 그리고 diamond.utils라는 세 가지 모듈과 상호작용함을 보았다. 사실 utils하위 패키지에 포함된 모든 클래스와 함수를 모두 util.py 모듈에 모아 하나의 거대한 파일로 만들 수 있지만, Diamond 개발팀은 네임스페이스를 사용하여 기능별로 코드를 분리했다. 대박!

#### 사용자가 확장할 수 있는 사용자 정의 클래스(복잡함이 꼬인 것보다 낫다)

새 콜렉터를 구현하는 작업은 쉽다. 그저 diamond.collector.Collector **추상 베이스 클래스**를 상속하여 Collector.collect() 메서드를 구현한 뒤, 구현 결과를 폴더에 담아 venv/src/collectors/에 넣어주면 된다. 

#### Diamond 스타일 예시 

#### 클로저 사용 예시(갓차가 갓차가 아닌 경우)

클로저는 지역 변수를 사용하는 함수이며, 해당 지역 변수가 정의된 함수가 호출되지 않는 한 클로저 함수르 사용할 수 없다. 다른 언어에서는 클로저는 구현하거나 이해학기 어려울 수 있지만, 파이썬에서는 그렇지 않다. 파이썬은 함수를 여타 객체처럼 다루기 때문이다. 예를 들어, 파이썬의 함수는 다른 함수의 인자 혹은 반환 값이 될 수 있다. 

```
##~~ ... 임포트 구문 생략 ... # 1번

def main():
    try:
        ##~~ ... 명령줄 파서 구현 생략 ...

        # Parse Command Line Args
        (options, args) = parser.parse_args()

        ##~~ ... 구성 파일을 파싱하는 코드 생략 ...
        ##~~ ... 로그를 구성하는 코드 생략 ...

    # Pass the exit up stream rather then handle it as an general exception
    except SystemExit, e:
        raise SystemExit

    ##~~ ... 구성에 관한 기타 예외 처리 코드 생략 ...
    
    try:
        # PID MANAGEMENT # 2번
        if not options.skip_pidfile:
            # Initialize Pid file
            if not options.pidfile:
                options.pidfile = str(config['server']['pid_file'])

            ##~~ ... PID 파일이 존재하면 이를 불러온 뒤, ...
            ##~~ ... 해당 PID의 프로세스가 없다면 파일을 삭제하고 ...
            ##~~ ... 해당 PID의 프로세스가 실행 중이라면 종료하는 코드 생략 ...
            
            ##~~ ... 그룹과 사용자 ID를 설정하는 코드와 ...
            ##~~ ... PID 파일 권한을 변경하는 코드 생략 ...
            
            ##~~ ... 데몬 여부를 확인한 뒤 ...
            ##~~ ... 만약 그렇다면 프로세스를 분리하는 코드 생략 ...

        # PID MANAGEMENT # 3번
        if not options.skip_pidfile:
            # Finish Initialize PID file
            if not options.foreground and not options.collector:
                # Write pid file
                pid = str(os.getpid())
                try:
                    pf = file(options.pidfile, 'w+')
                except IOError, e:
                    log.error("Failed to write child PID file: %s" % (e))
                    sys.exit(1)
                pf.write("%s\n" % pid)
                pf.close()
                # Log
                log.debug("Wrote child PID file: %s" % (options.pidfile))

        # Initialize Server
        server = Server(configfile=options.configfile)

        def sigint_handler(signum, frame): # 4번
            log.info("Signal Received: %d" % (signum))
            # Delete Pidfile
            if not options.skip_pidfile and os.path.exists(options.pidfile): # 5번
                os.remove(options.pidfile)
                # Log
                log.debug("Removed PID file: %s" % (options.pidfile))            
            sys.exit(0)

        # Set the signal handlers
        signal.signal(signal.SIGINT, shutdown_handler) # 6번
        signal.signal(signal.SIGTERM, shutdown_handler)

        server.run()

    # Pass the exit up stream rather then handle it as an general exception
    except SystemExit, e:
        raise SystemExit

    ##~~ ... 기타 예외 처리 코드 생략 ...
    ##~~ ... 나머지 코드 생략
```

- 1번: 요약 내용

- 2번: PID 파일을 통해 데몬이 고유한지 확인하고, 관련 프로세스 ID를 다른 스크립트에 신속히 전달한다.

- 3번: 이 부분은 클로저까지 이어지는 문맥을 제공하고자 남겼다. 이제 프로세스가 데몬화되어 이전과 다른 PID를 가진다. 

- 4번: sigint_handler() 함수는 클로저다. 최상위 수준이 아닌 main() 함수 안에 정의되어 있다. 이는 sigint_handler()가 PID 파일 탐색 여부와 그 위치를 알아야 하기 때문이다!

- 5번: 명령줄 옵션으로부터 조건문에 사용되는 정보를 얻는다. 이 정보는 main() 함수가 실행되기 전까지는 얻을 수 없다. 즉, PID 파일에 관한 모든 옵션은 main 네임스페이스의 지역 변수이다.

- 6번: 클로서(signal_handler() 함수)가 신호 핸들러에 전달되어 SIGINT와 SIGTERM을 처리하는 데 사용한다. 

### Tablib

Tablib은 데이터 형식을 바꾸거나, Dataset 객체에 데이터를 저장하거나, Datebook에 여러 Dataset을 저장하는 파이썬 라이브러리이다. 

#### 작은 라이브러리 읽기

Tablib은 애플리케이션이 아닌 라이브럴리이다. 따라서 HowDoI나 Diamond와 달리 진입점이 여러 개이다.

#### Tablib 사용하기

Tablib은 파이썬 대화형 세션에서 help() 함수를 사용하여 API를 탐색할 수 있다. 

다음은 tablib.Dataset 클래스를 사용해 여러 형식의 데이터를 불러오거나 저장하는 코드이다. 

```
>>> import tablib
>>> data = tablib.Dataset()
>>> names = ('Black Knight', 'Killer Rabbit')
>>> 
>>> for name in names:
... 	fname, lname = name.split()
... 	data.append((fname, lname))
...
>>> data.dict
>>> [['Black', 'Knight'], ['Killer', 'Rabbit']]
>>> 
>>> print(data.csv)
Black,Knight
Killer,Rabbit

>>> data.headers=('First name', 'Last name')
>>> print(data.yaml)
- {First name: Black, Last name: Knight}
- {First name: Killer, Last name: Rabbit}

>>> with open('tmp.csv', 'w') as outfile:
... 	outfile.write(data.csv)
...
64
>>> newdata = tablib.Dataset()
>>> newdata.csv = open('tmp.csv').read()
>>> print(newdata.yaml)
- {First name: Black, Last name: Knight}
- {First name: Killer, Last name: Rabbit}
```

#### Tablib 코드 읽기

모듈의 문서화 문자열을 통해 기존과 다른 방식으로 소스 코드를 둘러보자. 

다음과 같이 터미널 셸에서 패키지의 최상위 디렉터리로 이동한 뒤 head *.py를 입력하면, 모든 모듈의 문서화 문자열을 한꺼번에 볼 수 있다. 

```
(venv)$ cd tablib
(venv)$ head *.py
==> __init__.py <== # 1번
""" Tablib. """

from tablib.core import (
	Databook, Dataset, detect, import_set, import_book,
	InvalidDatasetType, InvalidDimensions, UnsupportedFormat,
	__version__
)

==> compat.py <== # 2번
# -*- coding: utf-8 -*-

"""
tablib.compat
~~~~~~~~~~~~~
Tablib compatiblity module.
"""

==> core.py <== # 3번
# -*- coding: utf-8 -*-
"""
	tablib.core
	~~~~~~~~~~~
	
	This module implements the central Tablib objects.
	
	:copyright: (c) 2014 by Kenneth Reitz.
	:license: MIT, see LECENSE for more details.
"""
```

- 1번: 최상위 수준 API에는 딱 아홉 개의 진입점이 있다. 먼저 Dataset과 Databook 클래스는 문서에 언급되어 있다. 일단 detect는 형식을 식별하는 것처럼 보이고, import_set과 import_book은 데이터를 불러올 게 분명하다. 그리고 나머지 세 클래스 InvalidDataType, InvalidDataDimensions, UnsupportedFormat는 예외처럼 보인다.

- 2번: tablib/compat.py는 호환성 모듈이다. 해당 모듈의 코드를 훑어보면, 파이썬 2와 3의 호환 문제를 처리하기 위해 tablib/core.py에서 사용하는 모듈의 위치나 이름 차이를 해결한다는 점을 쉽게 알 수 있다. 이는. HowDoI와 비슷한 해결법이다. 

- 3번: tablib/core.py에는 모듈 이름에서 알 수 있듯 Dataset과 Databook과 같은 핵심 Tablib 객체가 구현되어 있다. 

#### Tablib의 구조 예시

Tablib에서 가장 주목할 점은 tablib/formats/ 안의 모듈에 클래스가 없다는 것이다. 이는 클래스를 남용하지 않는 완벽한 예시이다. 

#### 형식적으로 불필요한 객체지향 코드는 필요 없다(함수 그룹화를 위해 네임스페이스를 사용하자)

grep^def formats/*.py를 사용하면 각 모듈이 다음 함수 중 일부 혹은 전부를 담고 있음을 알 수 있다. 

- detect(stream)은 스트림 내용에 기반하여 파일 형식을 유추한다. 

- dset_sheet(dataset, ws)는 엑셀 스프레드시트 셀의 서식을 지정한다. 

- export_set(dataset)은 Dataset을 주어진 형식으로 내보내며, 형식이 갖춰진 문자열을 반환한다. 

- import_set(dset, in_stream, headers=True)는 Dataset의 내용을 입력 스트림 내용으로 바꾼다. 

- export_set(dset, in_stream, headers=True)는 Databook 안의 Datasheet를 주어진 형식으로 내보내며, 문자열이나 bytes 객체를 반환한다. 

- import_book(dbook, in_stream, headers=True) Databook의 내용을 입력 스트림 내용으로 바꾼다. 

#### Tablib의 스타일 예시 

#### 연산자 오버로딩(아름다움이 추함보다 좋다)

Tablib은 파이썬의 연산자 오버로딩을 사용하여 Dataset의 행 단위/열 단위 연산을 가능하게 했다. 

```
>>> data[-1] # 1번
('1 whole', 'olive')
>>>
>>> data[-1] = ['2 whole', 'olives'] # 2번
>>> 
>>> data[-1]
('2 whole', 'olives') # 3번
>>>
>>> del data[2:7] # 4번
>>> 
>>> print(data.csv)
amount,ingredient # 5번
1 bottle,0l' Janx Spirit
1 measure,Santraginus V seawater
2 whole,olives

>>> data['ingredient'] # 6번
["Ol' Janx Spirit", 'Santraginus V seawater', 'olives']
```

- 1번: 대괄호 연산자([])와 숫자를 함께 사용하면, 특정 위치의 행 데이터에 접근할 수 있다. 

- 2번: 중괄호 연산자를 사용해 값을 할당할 수 있다. 

- 3번: 그리고 원래의 값이 바뀐 것을 확인할 수 있다. 

- 4번: 슬라이스(slice)를 사용해 값을 삭제했다. 2:7은 2,3,4,5,6을 가리키며, 7은 포함되지 않는다. 

- 5번: 데이터가 csv형식으로 바뀌었다. 

- 6번: 열 이름을 통해 열 데이터에 접근할 수도 있다. 

### Requests

2011년 발렌타인데이에 케네스 레이츠는 파이썬 커뮤니티에 대한 애정을 담아 Requests 라이브러리를 공개했다. Requests 라이브러리의 (API 문서를 읽을 필요가 없을 정도로) 직관적인 API 디자인은 파이썬 커뮤니티의 마음을 단숨에 사로잡았다. 

#### Requests 문서 읽기

Requests는 몇 가지 함수와 특색있는 클래스, 키워드 인자 뭉치만을 사용하여 IETF의 HTTP 기준을 맞추고자 노력하였다. 

#### Requests 사용하기

Tablib과 마찬가지로 Requests 또한 문서화 문자열이 잘 정리되어 있어 온라인 문서를 굳이 읽지 않아도 무리가 없다. 

다음은 간략한 상호작용 예시이다. 

```
>>> import requests
>>> help(requests) # 사용법 설명문을 보면 requests.api를 살펴보라고 설명되어 있다.
>>> help(requests.api) # 자세한 API 설명을 보여준다.
>>> 
>>> result = request.get('https://pypi.python.org/pypi/requests/json')
>>> result.status_code
200
>>> result.ok
True
>>> result.text[:42]
'{\n 	"info": {\n
>>> 
>>> result.json().keys()
dict_keys(['info', 'releases', 'urls'])
>>>
>>> result.json()['info']['summary']
'Python HTTP for Humans.'
```

#### Requests 스타일 예시 

Requests의 스타일은 집합을 사용하는 방법에 대한 좋은 예다(대개 집합은 자주 사용되지 않는다) requests.status_code 모듈은 전반적인 코드 스타일을 단순화하기 위해 존재하며, 이 모듈로 인해 HTTP 상태 코드가 필요할 때마다 일일히 코드를 나열하지 않아도 된다. 

#### 집합과 집합 연산(파이썬스럽고 멋진 관용구)

다음은 cookies.py에서 가져온 코드다. 함수 끝부분에서 집합 연산을 확인할 수 있다.

```
# 
# ... cookies.py에서 가져온 코드 ...
# 

def create_cookie(name, value, **kwargs): # 1번
    """Make a cookie from underspecified parameters.
    By default, the pair of `name` and `value` will be set for the domain ''
    and sent on every request (this is sometimes called a "supercookie").
    """
    result = dict(
        version=0,
        name=name,
        value=value,
        port=None,
        domain='',
        path='/',
        secure=False,
        expires=None,
        discard=True,
        comment=None,
        comment_url=None,
        rest={'HttpOnly': None},
        rfc2109=False,)

    badargs = set(kwargs) - set(result) # 2번
    if badargs:
        err = 'create_cookie() got unexpected keyword arguments: %s'
        raise TypeError(err % list(badargs)) # 3번

    result.update(kwargs) # 4번
    result['port_specified'] = bool(result['port']) # 5번
    result['domain_specified'] = bool(result['domain'])
    result['domain_initial_dot'] = result['domain'].startswith('.')
    result['path_specified'] = bool(result['path'])

    return cookielib.Cookie(**result) # 6번
```    

- 1번: **kwargs를 사용하여 사용자가 쿠키에 대한 키워드 인자를 자유로이 넘기거나 넘기지 않을 수 있게 한다. 

- 2번: 집합 연산이다! 파이썬스럽고 단순하다. 표준 라이브러리에 있다. 딕셔너리에 set()을 적용하면 키로 구성된 집합이 된다. 

- 3번: 긴 줄의 코드를 짧은 두 줄로 쪼갠 훌륭한 예다. err 변수가 추가됐지만 별 영향은 없다. 

- 4번: result.update(kwargs)는 result 딕셔너리를 kwargs 딕셔너리의 키/값 쌍으로 업데이트하며, 기존 쌍이 존재하면 값을 업데이트하고 그렇지 않으면 새로 만든다. 

- 5번: bool()을 호출하여 객체가 의미 있으면 True를 반환한다

- 6번: cookielib.Cookie를 초기화하려면 시그니처상 18개의 위치 인자와 1개의 키워드 인자가 필요하다. 따라서 Requests는 위치 인자를 키워드 인자처럼 사용할 수 있도록 딕셔너리 형태로 전달한다. 

### Werkzeug

Werkzeug 코드를 읽으려면 웹 서버가 애플리케이션과 통신하는 방법에 대해 조금 알아야 한다. 다음 문단에 최대한 간략하게 요약해보았다. 

1. 서버는 HTTP 요청을 받을 때마다 애플리케이션을 한번 호출한다.

2. 애플리케이션은 서버가 HTTP 요청에 대한 응답으로 사용할 순회 가능한 바이트 문자열을 포함한다.

3. 문서에 따르면 애플리케이션은 두 개의 파라미터를 받는다. 

2007년에 아르민 로나허는 WSGI라이브러리에 대한 염원과 필요를 충족시켜줄 백자이크(Werkzeug)를 배포했다. 백자이크는 WSGI 애플리케이션과 미들웨어 컴포넌트를 만드는 데 사용할 수 있다. 

#### 툴킷 코드 읽기

소프트웨어 툴킷은 호환 가능한 유틸리티의 모음이다. Werkzeug의 경우, WSGI 애플리케이션과 연관된 모든 게 소프트웨어 툴킷이 된다. 

#### Werkzeug 사용하기

Werkzeug는 WSGI 애플리케이션을 위한 여러 유틸리티를 제공한다. 

Werkzeug에는 일회용 테스트를 수행할 때 실제 웹서버를 대신하기 위한 werkqeug.client 클래스가 구현되어 있다. 클라이언트의 응답은 response_wrapper 인자 타입을 가진다. 

#### Werkzeug 코드 읽기 

테스트 커버리지가 좋다면 단위 테스트만 보고도 라이브러리의 역할과 기능을 알 수 있다. 단위 테스트를 볼 때는 의식적으로 '숲'이 아닌 '나무'를 봐야 한다는 점을 주의하자. werkzeug/test_routing.py를 열어 임포트한 객체를 찾아보자 이를 통해 모듈간 상호 연결을 빠르게 살필 수 있다. 

```
import pytest # 1번

import uuid # 2번

from tests import strict_eq # 3번

from werkzeug import routing as r # 4번
from werkzeug.wrappers import Response # 5번 
from werkzeug.datastructures import ImmutableDict, MultiDict # 6번
from werkzeug.test import create_environ # 7번
```

- 1번: 여기서는 테스트를 위해 pytest를 사용했다. 

- 2번: uuid 모듈은 test_uuid_converter() 함수에서만 사용된다. 이 함수는 문자열을 uuid.UUID 객체로 변환하는 기능이 잘 작동하는지 테스트한다. 

- 3번: strict_eq() 함수는 werkzeug/tests/__init__.py에 정의되어 있는 테스트용 함수이며, 자주 사용된다. 

- 4번: werkzeug.routing 모듈이 테스트 대상이다. 

- 5번: Respond 객체는 test_dispatch() 함수에서만 사용된다. 

- 6번: 여기에서 불러온 딕셔너리 객체는 한 번씩만 사용된다. ImmutableDict는 werkzeug.routing.Map의 변경 불가능한 딕셔너리가 정말 변경할 수 없는지 확인하는 데 사용하며, MultiDict는 여러 키 값을 URL 빌드 도구에 제공했을 때 알맞은 URL을 빌드하는지 확인하는 데 사용한다. 

- 7번: create_environ()는 테스트를 위한 함수이며, 실제 HTTP 요청을 사용하지 않고도 WSGI 환경을 만든다. 

#### Werkzeug 스타일 예시 

#### 자료형을 추측하는 우아한 방법(구현 결과를 설명하기 쉽다면, 그 아이디어는 좋은 아이디어일 수 있다)

텍스트 파일을 파싱하여 여러 자료형으로 변환해야 하는 작업은 자주 필요하다. 이에 대한 Werkzeug의 해답은 유독 파이썬스러우며, 스타일 예시로 소개하기 적절하다. 

```
_PYTHON_CONSTANTS = {
	'None':	None,
	'True': 	True,
	'False': 	False
}

def _pythonize(value):
	if value in _PYTHON_CONSTANTS: # 1번
		return _PYTHON_CONSTANTS[value]
	for convert in int, float: # 2번
		try: # 3번
			return convert(value)
		except ValueError:
			pass
	if value[:1] == value[-1:] and value[0] in '"\'': # 4번
		value = value[1:-1]
	return text_type(value) # 5번
```

- 1번: 파이썬 딕셔너리는 키를 검색 할 때 해시 함수를 집합처럼 사용한다. 대신, 파이썬 사용자는 if/elif/else를 사용하거나, 예시 코드처럼 딕셔너리 탐색을 사용한다. 

- 2번: float보다 제한적인 자료형인 int를 먼저 반환하는 점에 주목하자. 

- 3번: 자료형을 추론하기 위해 try/except문을 사용했다. 파이썬 스럽다. 

- 4번: 이 부분은 꼭 필요한 부분이다. 코드는 werkzeug/routing.py에 있고, 파싱되는 문자열은 URL의 일부이기 때문이다. 

- 5번: text_type은 문자열을 유니코드로 변환한다. 이때, 파이썬 2와 3에서 모두 호환되는 방식으로 변환된다. 

#### Werkzeug 구조 예시

#### 클래스기반 데코레이터(동적 타이핑의 파이썬스러운 사용)

Werkzeug는 덕 타이핑을 사용하여 @cached_property 데코레이터를 만들었다. Tablib 프로젝트에서는 프로피티가 함수처럼 정의되었음을 떠올려보자. 대체로 데코레이터는 함수이다. 그러나 형식에 대한 제한이 없기 때문에, 호출 가능한 객체라면 얼마든지 데코레이터가 될 수 있다. 

- 다음은 사용 예시이다. 

```
>>> from werkzeug.utils import cached_property
>>> 
>>> class foo(object):
... 	@cached_property
... 	def foo(self):
... 		print("You have just called Foo.foo()!")
... 		return 42
...
>>> bar = foo()
>>> 
>>> bar.foo
You have just called Foo.foo():
42
>>> bar.foo
42
>>> bar.foo # 더이상 출력문이 작동하지 않음에 주의하자 
42
```

#### Response.__call__

Requests 라이브러리와 마찬가지로, Response 클래스는 BaseResponse에 여러 기능을 더하여 만들어졌다. 

#### 믹스인(네임스페이스 못지 않게 대박 좋은 아이디어다)

파이썬의 믹스인은 클래스에 특정 기능을 추가하기 위해 사용하는 클래스다. 파이썬은 자바와 달리, 다중 상속이 허용된다. 즉, 클래스는 만들 때 여러 개의 서로 다른 상위 클래스로부터 여러 가지 행동이나 특징을 상속받아 만들 수 있고, 여러 기능을 클래스별로 구분하여 모듈화 하는게 가능해진다. 일종의 '네임스페이스'라 볼 수 있겠다. 

때때로 Werkzeug의 믹스인 메서드에 특정 속성이 필요할 수 있다. 이러한 요구사항은 대부분 믹스인 문서화 문자열에 설명되어 있다. 

```
# ... in werkzeug/wrappers.py

class UserAgentMixin(object): # 1번

    """Adds a `user_agent` attribute to the request object which contains the
    parsed user agent of the browser that triggered the request as a
    :class:`~werkzeug.useragents.UserAgent` object.
    """

    @cached_property
	 def user_agent(self):
    """The current user agent."""
    from werkzeug.useragents import UserAgent
    return UserAgent(self.environ) # 2번
    
    class Request (BaseRequest, AcceptMixin, ETagRequestMixin, 
    					UserAgentMixin, AuthorizationMixin, # 3번
    					CommonRequestDescriptorsMixin): 
		"""Full featured request object implementing the following mixins: 
		
		- :class:`AcceptMixin` for accept header parsing 
		- :class:`ETagRequestMixin` for etag and cache control handling 
		- :class:`UserAgentMixin` for user agent introspection 
		- :class:`AuthorizationMixin` for http auth handling 
		- :class:`CommonRequestDescriptorsMixin`
		"""
		# 4번
```

- 1번: UserAgentMixin은 특별할 게 없다. 파이썬 3에서는 object를 상속하는 게 기본값이지만, 파이썬 2와의 호환성을 위해 명시하였다.

- 2번: UserAgentMixin.user_agent는 self.environ 속성이 있다고 가정한다. 

- 3번: Request를 위한 베이스 클래스 목록에 믹스인이 포함되면, Request(environ).user_agent를 통해 믹스인의 속성에 접근할 수 있다. 

- 4번: 정말 별게 없다. Requests를 정의한 코드는 여기서 끝난다. 모든 기능은 베이스 클래스나 믹스인에서 제공된다. 

### Flask 

Flask는 Werkzeug와 Jinja2를 결합한 웹 마이크로 프레임워크다. 농담처럼 만들어져 2010년 만우절에 배포되었지만, 금새 파이썬에서 가장 인기 있는 웹 프레임워크 중 하나가 되었다. 

#### 프레임워크 코드 읽기

소프트웨어 프레임워크는 물리적인 프레임워크와 같다. Flask는 WSG 애플리케이션을 빌드하는 데 필요한 기반 구조를 제공하며, 라이브러리 사용자는 그 위에 Flask 애플리케이션이 작동하도록 컴포넌트를 쌓아 사용한다. 

#### Flask 사용하기 

#### Flask 코드 읽기

Flask의 궁극적인 목적은 웹 애플리케이션을 만드는 것이다. 따라서 Diamond나 HowDoI와 같은 명령줄 애플리케이션과 그리 다르지 않다. 

먼저 flaskr.py에 중단점을 추가해보면 코드가 실행되다가 중단점에 도달하면 대화형 세션에서 디버거에 진입한다. 

```
@app.route('/') 
def show_entries():
	import pdb ; pdb.set_trace() ## 중단점이 되는 코드
	db = get_db() 
	cur = db.execute('select title, text from entries order by id desc') 
	entries = cur.fetchall()
	return render_template('show_entries.html', entries = entries)
```

다음으로는 파일을 닫고 명령줄에 python을 입력하여 대화형 세션에 들어가자. 

서버를 시작하기보다, Flask 내부 테스팅 유틸리티를 사용하여 HTTP GET 요청을 디버거가 위치한 /에 시뮬레이션하자. 

```
>>> import flaskr 
>>> client = flaskr.app.test_client() 
>>> client.get('/')
> /[...truncated path ...]/flask/examples/flaskr/flaskr.py(74)show_entries()
-> db = get_db()
(Pdb)
```

#### Flask 스타일 예시 

#### Flask의 라우팅 데코레이터(아름다움이 추함보다 좋다)

Flask의 라우팅 데코레이터는 아래와 같이 대상 함수에 URL 라우팅을 추가한다. 

```
@app.route('/')
def index():
	pass
```

Flask 애플리케이션은 요청을 보낼 때 URL 라우팅을 사용하여 응답을 생성하는 함수가 올바른지 분별한다. 데코레이터 구문은 라우팅 코드 로직을 대상 함수에서 제외시킴으로써 함수 구조를 수평적으로 만드는 데 도움이 되며, 사용하기 쉽다. 

다음은 flask/flask/app.py의 메인 Flask 클래스의 메서드 소스 코드이다!

```
class Flask(_PackageBoundObject): # 1번
	"""The flask object implements a WSGI application ... 
	... 문서화 문자열의 나머지 부분은 생략함 ... 
	""" 
	##~~ ... routing() 메서드를 제외한 나머지 생략.
	
	def route(self, rule, **options):
		"""A decorator that is used to register a view function for a 
		given URL rule. This does the same thing as :meth:`add_url_rule` 
		but is intended for decorator usage:: 
	
	@app.route('/') 
	def index(): 
		return 'Hello World' 
	
	... 나머지 문서화 문자열 생략 ... 
	""" 
	def decorator(f): # 2번
		endpoint = options.pop('endpoint', None) 
		self.add_url_rule(rule, endpoint, f, **options) # 3번
		return f 
return decorator	
```

- 1번: _PackageBoundObject는 HTML 템플릿, 정적 파일 등을임포트하기 위한 파일 구조를 설정하며, 애플리케이션 모듈 위치에 대한 상대 경로를 특정 짓는 구성 값을 사용한다. 

- 2번: 데코레이터니까 데코레이터라고 이름을 붙였다.

- 3번: 모든 규칙을 담은 매핑에 URL을 추가하는 함수 부분이다. Flask.route의 유일한 목적은 라이브러리 사용자에게 편리한 데코레이터를 제공하는 것이다. 

#### Flask 구조 예시

Flask의 구조 예시 주제는 모듈성이다. Flask는 쉽게 확장하고 수정할 수 있게 설계되었다. 거의 모든 것이 쉽게 수정할 수 있으며, 여기서 거의 모든 것이란 JSON 문자열을 인코딩하고 디코딩하는 방법부터 URL을 라우팅하는 데 사용하는 클래스까지 다양하다.

#### 애플리케이션 전용 기본 값(단순함이 복잡함보다 좋다)

Flask와 Werkzeug 둘 다 wrapper.py 모듈을 가진다. Flask는 웹 애플리케이션 전용 프레임워크이며, Werkzeug는 WSGI 애플리케이션을 위한 보다 범용적인 유틸리티 라이브러리이다. Flask의 wrapper.py는 Werkzeug 위에 Flask 전용 기본 값을 추가하기 위해 존재한다. 이때, 웹 애플리케이션에 관한 특정 기능을 추가하기 위해 Werkzeug의 Request와 Response 객체를 상속한다. 예를 들어, flask/flask/wrappers.py의 Response 객체는 다음과 같이 생겼다. 

```
from werkzeug.wrappers import Request as RequestBase, Response as ResponseBase
##~~ ... 나머지 코드 생략 ...

class Response(ResponseBase):  # 1번
    """The response object that is used by default in Flask.  Works like the
    response object from Werkzeug but is set to have an HTML mimetype by
    default.  Quite often you don't have to create this object yourself because
    :meth:`~flask.Flask.make_response` will take care of that for you.

    If you want to replace the response object used you can subclass this and
    set :attr:`~flask.Flask.response_class` to your subclass. # 2번
    """
    default_mimetype = 'text/html' # 3번
```

- 1번: Werkzeug의 Response 클래스를 ResponseBase로 임포트하여 그 역할을 분명히 하고, Response라는 이름의 새로운 서브 클래스를 만들 수 있도록 했다. 멋진 스타일이다!

- 2번: flask.wrappers.Response란 이름의 서브 클래스를 만들고 사용하는 방법이 문서화 문자열에 나와 있다. 이와 같은 기능을 구현할 때, 문서화를 잊지 말자. 문서가 없으면 사용자가 이를 사용할 가능성이 낮아 진다. 

- 3번: Response 클래스에서 이 부분만 바뀌었다. Request 클래스에서는 더 많은 변경사항이 있지만, 설명이 너무 길어지니 생략한다. 

#### 모듈성(네임스페이스 못지 않게 대박 좋은 아이디어다)

flask.wrappers.Response의 문서화 문자열은 사용자로 하여금 Response 객체를 상속 받아 메인 Flask 객체 내에 사용자가 입맛에 맞는 새클래스를 정의하여 사용할 수 있도록 한다. 






