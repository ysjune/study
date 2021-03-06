## 2. 의미 있는 이름

#### 의도를 분명히 밝혀라
로직이 간단한 것보단, 이름이 간단 명료한 것이 좋다.
<br/><br/>
#### 그릇된 정보를 피하라
유사한 개념은 유사한 표기법을 사용한다.<br/> 
일관성이 떨어지는 표기법은 그릇된 정보이다.<br/> 
개발자는 대부분 
**(객체에 달린 상세한 주석이나 제공하는 다른 목록을 보고 선택하기 보다는 이름만 보고 객체를 선택하는 경우가 대다수이다.)**
<br/><br/>
#### 의미있게 구분하라  
customerInfo 와 customer / accountData 와 account 는 구분이 가지 않는다.<br/>
읽는 사람이 차이를 알도록 이름을 지어라.
<br/><br/>
#### 발음하기 쉬운 이름을 사용하라
genymdhms (generate date, year, month, day, hour, minute, second) 라는 단어의 조합은 발음하기도 어렵고, 토론하기도 어렵다.
<br/><br/>
#### 검색하기 쉬운 이름을 사용하라
 이름을 의미있게 지으면 함수가 길어지긴 하지만, 찾기는 쉬워진다.<br/>
 그냥 상수나 글자 하나의 변수를 사용하는 것보단 훨씬 낫다.
<br/><br/>
#### 자신의 기억력을 자랑하지 마라
일반적으로 문제 영역이나 해법 영역에서 사용하지 않고, <br/>
자신이 아는 이름으로 변수를 작성한다면 나중에 문제가 생기기 마련이다.<br/>
for 등을 사용하는 반복문을 제외하고는 i,j,k 등을 사용하지 않는 것이 바람직하다. 
<br/><br/>
#### 클래스 이름
클래스 이름과 객체 이름은 명사나 명사구가 적합하다. <br/>
Customer, Account 등.. Info 등과 같은 단어는 피하고, 동사는 사용하지 않는다.
<br/><br/>
#### 매서드 이름
매서드 이름은 동사나 동사구가 적합하다. <br/>
postPayment, deletePage 등이 좋은 예이다.
<br/><br/>
#### 기발한 이름은 피하라
재미난 이름보다 명료한 이름을 선택하는 것이 좋다.
<br/><br/>
#### 한 개념에 한 단어를 사용하라
추상적인 개념 하나에는 단어 하나를 선택해 이를 고수해라. <br/>
예를 들어 똑같은 클래스마다 get, fetch, retrieve 등을 사용하면 혼란을 야기할 수 있다. 
<br/><br/>
#### 말장난을 하지 마라
한 단어를 두 가지 목적으로 사용하지 마라. <br/>
예를 들어 add 라는 기존에는 두 값을 더해서 값을 구하는 메소드가 있을 때, <br/>
집합에 값 하나를 추가하는 메소드는 add 와는 맥락이 다르므로 insert 나 append 라는 이름이 적당하다.
<br/><br/>
#### 해법영역에서 가져온 이름을 사용하라
코드를 작성하는 사람도 코드를 읽는 사람도 프로그래머이다. 기술 개념에는 기술 이름이 가장 적합한 선택이다. <br/>
Ex) singleton, factory
<br/><br/>
#### 불필요한 맥락은 없애라
예를 들어 휘발유 충전소 라는 애플리케이션을 만든다고 해서 모든 클래스 앞에 GSD 를 붙인다면 이는 불필요한 맥락이다. 
<br/><br/>
#### 결론
우리들 대다수는 자신이 짠 클래스 이름과 매서드 이름을 모두 암기하지 못한다. <br/>
그렇기 때문에 문장이나 문단처럼 읽히는 코드 아니면, 적어도 표나 자료 구조처럼 읽히는 코드를 짜는 데에 집중해야 한다.
<br/><br/>
#### 사견을 덧붙이면...?
개인적으로는 가장 공감하면서도 지키려고 하는 챕터의 내용이다. <br/>
그리고.. 어려운 부분이기도 하다. <br/>
여러 주의점들이 있겠지만, 나에게는 <br/> 
특히 **말장난을 하지 마라** 이 부분이 가장 주의해야 할 부분이 아닌가 싶다. <br/>
개인적으로 스프링으로 개발을 할 때, <br/>
서비스 계층은 add 등의 일반적인 용어를 사용하고 Persistent 계층은 DB 친화적인 단어를 사용하여 insert 를 사용한다. <br/>
그러다보면 종국에는 만능 add 와 만능 insert 가 되는 느낌이 들곤 하는데... <br/>
내 나름대로도 어떤 상황에서는 어떤 단어로 통일하자는 그런 개념? 이 확립되어야 할 것 같다.
