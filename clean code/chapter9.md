## 9. 단위 테스트

#### TDD 의 법칙 3가지
1. 실패하는 단위 테스트를 작성할 때까지 실제 코드를 작성하지 않는다.
2. 컴파일은 실패하지 않으면서 실행이 실패하는 정도로만 단위 테스트를 작성한다.
3. 현재 실패하는 테스트를 통화할 정도로만 실제 코드를 작성한다.


#### 깨끗한 코드 유지하기
지저분한 코드를 내놓으나 테스트를 안 하나 오십보 백보이다. <br/>
그 이유는 실제 코드가 진화하면 테스트 코드도 변해야 하기 때문이다. <br/>
그런데 테스트 코드가 지저분하면 그만큼 수정하기가 어려워진다. <br/>
테스트 코드는 실제 코드 못지 않게 중요하다. 테스트 코드는 이류 시민이 아니다. <br/>
실제 코드 못지 않게 깨끗하게 짜야 한다.


#### 테스트는 유연성, 유지보수성, 재사용성을 제공한다.
테스트 코드를 깨끗하게 유지하지 않으면 결국은 잃어버린다. <br/>
그리고 테스트 케이스가 없으면 실제 코드를 유연하게 만드는 버팀목도 사라진다. <br/>
테스트 케이스가 없다면 모든 변경은 잠정적인 버그다. 


#### 깨끗한 테스트 코드
깨끗한 테스트 코드를 만들려면 세 가지가 필요하다. 가독성!, 가독성!!, 가독성!!! <br/>
테스트 코드는 최소의 표현으로 많은 것을 나타내야 한다. 


#### 이중 표준
테스트에 적용하는 표준은 실제 코드에 적용하는 표준과는 확실히 다르다. <br/>
단순, 간결, 표현력 풍부해야 하지만, 실제 코드만큼 효율적일 필요는 없다. <br/>
실제 환경에서는 절대로 안되지만, 테스트 환경에서는 전혀 문제 없는 방식이 있다. <br/>
대게 메모리나 CPU 효율과 관련 있는 경우다. 코드의 깨끗함과는 무관한 케이스이다.


#### 테스트 당 개념 하나
테스트 함수마다 한 개념만 테스트하라 이것저것 잡다한 개념을 연속으로 테스트하는 긴 함수는 피해야한다.


#### F.I.R.S.T
- First : 테스트는 빨라야 한다. 테스트가 느리면 자주 돌릴 엄두를 못 내고, 자주 돌리지 않으면 초반에 문제를 찾아내 고치지 못한다.
- Independent : 각 테스트는 서로 의존하면 안된다. 한 테스트가 다음 테스트가 실행될 환경을 준비해서는 안된다. 각 테스트는 독립적으로 그리고 어떤 순서로 실행해도 괜찮아야 한다. 
- Repeatable : 테스트는 어떤 환경에서도 반복 가능해야 한다. 어느 환경에서든 실행할 수 있어야 한다. 그렇지 않으면 변명거리를 만들게 된다.
- Self-Validating : 테스트는 부울 값으로 결과를 내야 한다. 성공 아니면 실패다. 통과 여부를 알려고 로그 파일을 읽게 만들어서는 안된다. 테스트가 스스로 성공과 실패를 가늠하지 않는다면 판단은 주관적이 되며 지루한 수작업 평가가 필요하게 된다.
- Timely : 테스트는 적시에 작성해야 한다. 단위 테스트는 테스트하려는 실제 코드를 구현하기 직전에 구현한다. 

#### 결론
사실상 깨끗한 테스트 코드라는 주제는 책 한 권을 할애해도 모자랄 주제다. <br/>
테스트 코드는 실제 코드만큼이나 프로젝트 건강에 중요하다. <br/>
테스트 코드가 방치디어 망가지면 실제 코드도 망가진다. 테스트 코드를 깨끗하게 유지하자.


#### 사견을 덧붙이면...?
테스트 코드까지 왔다. 테스트 코드는 말로만 들었지, 실제로 접해본 건 5개월 정도 전이다. <br/>
그 전에는 테스트 코드가 뭔지 몰랐고, 뭔지 안 시점에서는 어떻게 적용해야할지 몰랐다. (뭐, 지금도 잘 하는 건 아니지만) <br/>
전 장에서도 언급했지만, 유닛 테스트 하면 역시 리펙토링이 떠오르게 된다. <br/>
개인적으로는 리펙토링 스터디를 통해 좋은 테스트 코드 작성법을 알게 된 것 같다. <br/>
이전에는 테스트 코드를 한 프로세스를 테스트 한다는 개념으로 작성했었다. 그러다보니 시간이 길게 걸리고 메소드 하나하나에 대한 검증이 쉽지 않았다. <br/>
그런 코드를 가지고 발표를 진행하는데 들었던 얘기가 여기에 나와 있는 말과 같다 **테스트 당 개념 하나** <br/>
아마 다른 건 몰라도 이 개념은 계속 지켜나가지 않을까?
