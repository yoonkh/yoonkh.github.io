---
layout: post
title:  "List와 array의 차이점"
date:   2018-01-03
author: Yoonkh
categories: Code
tags:	
- Python
- Code
- Algorithm
- Array
comments: True
---

# List와 Array의 차이점 

- 배열의 장점: 인덱스가 있어서 데이터의 접근이 빠르다. 
- 배열의 단점: 인덱스 <-> 데이터 매핑 구조이기 때문에, 데이터가 삭제되면 해당 공간이 낭비된다. 

List는 배열의 index라는 장점을 버리고, 빈틈없는 데이터의 적재라는 장점을 취한 자료구조이다. 

배열에 데이터를 추가하려면 기존에 있는 데이터 혹은 인덱스와 매핑된 자리에만 데이터를 삽입할 수 있다. 
![](http://cfile10.uf.tistory.com/image/2216FE4D562AD89B1B38BE)

리스트의 경우,
![](http://cfile3.uf.tistory.com/image/23555F3F562AD89D277968)


인덱스가 하나씩 밀리면서 순서를 유지한다. 

결론적으로 List에서는 인덱스보다, 데이터들 간의 순서를 더 중요시한다. 
