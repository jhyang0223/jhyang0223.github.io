---
layout: post
title: 내가 모르는 c++ 사용법
subtitle: 알고리즘 공부를 하면서 정리하는...
gh-repo: jhyang0223/jhyang0223.github.io
gh-badge: [star, fork, follow]
tags: [c++]
comments: true
---
### 해당 포스트의 목적
알고리즘을 공부하면서 까먹었던 C++(사용 안한지 5년...)에서 vector와 같은 c++에서 라이브러리 형태로 제공하는 자료구조 클래스(STL) 사용법등의 C++를 알고리즘 문제를 푸는 도구로 사용함에 있어서 문제 없도록 하는 것이 목적이다.

해당 포스트는 20210609에 처음 작성되었지만 이후에 C++ 코딩을 하면서 모르는 것이 생기거나 기록을 해야겠다고 생각되는 것을 꾸준히 업데이트 할 것이다.
## C++ 출력
### 소수점 자리 제한
C++을 이용하여 실수를 출력하다보면 소숫점 아래 몇 번째 자리까지 지정하여 출력하여야 하는 경우가 있다. 그 경우 출력문 이전에 아래와 같은 코드를 추가해주면 된다.
```
std::cout<<fixed;
std::cout.precision(7);
```

## C++ 입력
### cin 사용
#### 일반 cin 사용법
``` std::cin >> val; ```    
#### cin.getline()
엔터를 입력하는 순간 엔터 입력 이전의 문자열을 받는다. 공백도 포함하며, 만약 'my apple'이라는 문자열을 입력하고 엔터를 친다면 cin.getline(buff_val,len)는 해당 문자열 전부를 문자열 변수에 저장 시킬 수 있다. 

#### cin.get()   
문자 하나를 입력받아 저장할 수 있도록 한다. 공백 및 개행 문자도 받아올 수 있으며, 만약 'abc de'라는 문자열을 키보드로 입력한다면 'a', 'b', 'c', ' ', 'd', 'e' 총 여섯 번의 cin.get()함수 호출이 필요하다.

## C++ STL(Standard Template Library)
STL은 C++ 자료 구조 클래스 템플릿이라고만 알고 있었는데, 이를 STL 컨테이너라는 이름으로도 부른다. (맨날 도커 컨테이너 이런거 공부하다가 c++에서 컨테이너라는 단어를 들으니 상당히 낯설다...;;)

### vector
동적 배열과 동일한 동작을 하는 자료구조 클래스 템플릿. 메모리의 할당, 해제, 확장, 값의 삽입, 삭제 등의 배열 관리를 제공하는 함수를 통하여 편리하게 관리할 수 있다.
비슷한 컨테이너로는 array와 list가 있는데, 이는 추후에 정리하고 나서 비교를 해보는 것이 좋을 것 같다...

#### 생성자
- *vector<type> vtr;*       
  빈 벡터 vtr의 선언
- *vector<type> vtr(10);*         
  10개의 원소를 가지는 vector vtr을 선언하고, 초기화 함.(길이가 10인 배열을 생성한다고 보면 된다.) 원소의 초기화 값은 0이다.
- *vector<type> vtr(10,x);*          
  10개의 원소를 가지는 vector vtr을 선언하고, 초기화 함. 원소의 초기화 값을 x로 지정 함.
- *vector<type> vtr(vtr2);*             
  vector의 복사 생성자이다. (이게 복사 생성자였던 것 같은데... 했는데 맞았다. 그래도 조금이라도 기억하는거 같아서 기분 좋네...)

#### 연산자
연산자는 "==", "!=", "<", ">", "<=", ">=" 사용 가능하다. 즉, 대소 비교 가능   
그리고 첨자 연산자 [](subscript operator)가 일반 배열처럼 원소 참조 기능으로 사용 가능하다. *ex. vtr[2]*
#### 멤버 함수
(vector<type> vtr이 선언 되었을 때, 멤버 함수를 사용한다고 가정한다.)
- *vtr.assign(10, 2);*         
  생성자를 사용하지 않고, vector<type> vtr;로 선언만 되어있을 때, 초기화를 시켜주는 방법. 길이 10 vector를 생성 후, 2로 초기화.
- *vtr.at(idx);*   
  idx 번째 원소를 참조한다. 범위 점검 기능을 가지지만, 속도는 첨자 연산자 보다 느리다.
- *vtr.front();(vtr.back());*    
  첫 번째(마지막) 원소를 참조
- *vtr.clear()*   
  모든 원소 내용 삭제, 원소만 제거 하고 메모리에서 벡터를 없애는 것이 아님 (capacity는 그대로 있고, size만 0으로 줄어든다.)
- *vtr.push_back(5)*   
  마지막 원소 뒤에 원소 5를 삽입한다.
- *vtr.pop_back()*   
  마지막 원소 제거
- *vtr.begin(), vtr.end(), vtr.rbegin()*과 같은 iterator 연관 함수    

### 원소 탐색을 도와주는 iterator   
iterator는 자료 구조 클래스 템플릿(컨테이너)가 아니다. 하지만 개념을 좀 더 명확하게 기억하기 위하여 따로 정리하는 것이다.

#### iterator와 컨테이너
  iterator는 vector, deque, list와 같은 순차 컨테이너(sequence container)에서 사용되는 원소를 가리키는 포인터 개념의 객체다.    
  이 iterator라는 개념은 원소 for문 쓰면서 확인할 때 쓰던 것이 어렴풋하게 기억나고, python 쓰면서도 있었던 것 같다. (찾아보니 python, java 등에도 있는 개념이라고 한다.)    
  iterator의 선언은 아래와 같다.    
  선언 : ``` std::vector<int>::iterator iter; ```   
#### vector container에서 iterator 연관 함수들
  - *vtr.begin()*
  vector에서 첫번째 원소를 가리킨다.   
  - *vtr.end()*   
  vector에서 마지막 원소의 다음을 가리킨다. 즉, vector를 순차 탐색 할 때, vtr.begin()에서 시작하여 vtr.end()가 되기 전까지 탐색하여야 한다.   
  
  for문을 이용하여 vector의 원소를 순차 탐색하는 코드는 아래와 같다.
  
  ```
  std::vector<int>::iterator iter;
  
  for(iter = vtr.begin(); iter != vtr.end(); iter++) {
    std::cout << *iter <<endl;   
  }
  ```
  
## C++ 문자 및 문자열 처리
### 문자 ascii 코드 값

