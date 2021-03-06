## 13. 동시성

#### 동시성이 필요한 이유?
동시성은 커플링(결합)을 없애는 전략이다, 즉 무엇과 언제를 분리하는 전략이다 <br/>
단일 스레드의 경우 호출 스택을 살펴보면 프로그램 상태가 곧바로 드러난다. <br/>
응답 시간과 작업 처리량 혹은 한 번에 한 사람만 처리하는 경우, 정보를 대량으로 분석하는 경우, 이런 경우를 위해 동시성이 필요하다 할 수 있다.

#### 미신과 오해
 > - 동시성은 성능을 높여준다 (때때로 높여준다, 각 스레드가 독립적인 행동을 취할 때)
 > - 동시성을 구현해도 설계가 바뀌지 않는다 (단일과 다중 스레드 시스템은 설계가 판이하게 다름)
 > - 웹 또는 EJB 컨테이너를 사용하면 동시성을 이해할 필요가 없다 (오히려 더 알아야 한다. 동시 수정, 데드락 등을 피하기 위해)
 
#### 타당한 생각
 > - 동시성은 다소 부하를 유발한다 (성능 측면에서 부하가 걸리며, 코드도 더 짜야됨)
 > - 동시성은 복잡하다.
 > - 동시성 버그는 재현이 어렵다 (그렇기에 일회성 문제로 여겨 무시되는 경우가 생김)
 > - 동시성을 구현하려면 근본적인 설계 전략을 재고해야 됨

#### 난관
두 스레드가 있을 때 두 스레드가 자바 코드 한 줄을 거쳐가는 경로는 수 없이 많다. <br/>
대부분 올바른 결과를 내놓지만, 일부가 잘못된 결과를 내놓고, 이 경우가 드물다 <br/>

#### 동시성 방어 원칙

1. 단일 책임 원칙
동시성은 복잡성 하나만으로 충분히 분리할만한 가치가 있으며, 동시성을 구현할 때는 다음을 고려한다.

  > - 동시성 코드는 독자적인 개발, 변경, 조율 주기가 있다.
  > - 독자적인 난관이 있으며, 다른 코드에서 겪는 난관과는 난이도가 다르다.
  > - 잘못 구현된 코드는 별의 별 방식으로 실패한다.

  **권장사항** : 동시성 코드는 다른 코드와 분리하라. <br/>
  
2. 따름 정리 : 자료 범위를 제한하라
두 스레드가 공유하는 영역을 synchronized 키워드로 보호한다. 이런 임계영역의 수는 줄여야 하고, 공유 영역이 많아질 수록 다음 가능성도 커진다

  > - 보호할 임계영역을 빼먹어서 공유 자료를 수정하는 모든 코드를 망가뜨린다.
  > - 모든 임계영역을 보호했는지 확인하느라 똑같은 노력과 수고를 반복한다.
  > - 찾아내기 어려운 버그가 더 찾기 어려워진다.
  
  **권장 사항** : 자료를 캡술화 하고, 공유 자료를 최대한 줄여라<br/>
  
3. 따름 정리 : 자료 사본을 사용하라
공유 자료를 줄이려면 처음부터 공유하지 않는 방법이 최상이다. 이럴 경우 원본은 두고 사본을 사용하는 방법이 있는데 <br/>
객체를 복사하는 시간이 걸린다면 테스트를 통해 측정해본다. 하지만 사본으로 동기화를 피할 수 있다면 내부 잠금을 없애 절약한 수행 시간이 <br/>
사본 생성과 가비지 컬렉션에 드는 부하를 상쇄할 가능성이 크다.<br/>

4. 따름 정리 : 스레드는 가능한 독립적으로 구현하라
다른 스레드와 자료를 공유하지 않는다. 각 스레드는 클라이언트 요청 하나를 처리한다. 그러면 각 스레드는 세상에 자신만 있는 듯이 돌아갈 수 있다.<br/>
  
  **권장 사항** : 독자적인 스레드로, 가능하면 다른 프로세서에서 돌려도 괜찮도록 자료를 독립적인 단위로 분할하라.<br/>
  
#### 실행 모델을 이해하라

1. 생산자 - 소비자
생산자 스레드는 대기열에 정보를 채운 다음 소비자 스레드에게 "대기열에 정보가 있다"는 시그널을 보낸다. 소비자 스레드는 대기열에서 정보를 읽어들인 후 "대기열에 빈 공간이 있다" 는 시그널을 보낸다. 따라서 잘못하면 생산자 스레드와 소비자 스레드가 둘 다 진행 가능함에도 불구하고 동시에 서로에게서 시그널을 기다릴 가능성이 존재한다.

2. 읽기 - 쓰기
읽기 스레드의 요구와 쓰기 스레드의 요구를 적절히 만족시켜 처리율도 적당히 높고 기아도 방지하는 해법이 필요.<br/>
간단한 방법은 읽기가 없을 때까지 쓰기가 기다리는 방법이지만, 읽기가 지속될 경우 쓰기가 기아 상태에 걸린다. <br/>
반대로 쓰기 가 우선이 되면, 처리율이 떨어진다. 

3. 식사하는 철학자들
둥근 식탁에 철학자들이 앉아있고 각 철학자 왼쪽에는 포크가 있으며, 철학자는 스파게티를 먹을 때 양손을 사용. <br/>
철학자를 스레드로 포크를 자원으로 바꿔 생각해보라. 여러 프로세스가 자원을 얻으러 경쟁하기에, 주의해서 설계하지 않으면 데드락, 라이브락, 처리율 저하, 효율성 저하등을 겪는다.

  **권장 사항** : 설명한 3가지와 관련된 알고리즘과 각 해법을 이해해라
  
#### 동기화하는 메소드 사이에 존재하는 의존성을 이해하라
자바에서는 동기화를 위해 synchronized 를 지원하지만 공유 클래스 하나에 동기화된 메소드가 여럿이라면 구현이 올바른지 다시 한 번 확인해야된다.

  **권장 사항** : 공유 객체 하나에는 메소드 하나만 사용하라
  
하지만, 공유 객체 하나에 여러 메소드가 필요한 상황도 있다.

1. 클라이언트에서 잠금 : 클라이언트에서 첫 번째 메소드를 호출하기 전에 서버를 잠그고, 마지막 메소드를 호출할 때까지 유지한다.
2. 서버에서 잠금 : 서버에 "서버를 잠그고 모든 메소드를 호출한 후 잠금을 해제"하는 메소드를 생성, 클라이언트는 이 메소드를 호출
3. 연결 서버 : 잠금을 수행하는 중간 단계를 생성한다. 2.서버에서 잠금 과 다른 점은 서버를 변경하지 않는 것.

#### 동기화하는 부분을 작게 만들어라
자바에서 synchronized 를 사용하면 락이 설정된다. 락은 스레드를 지연시키고 부하를 가중시키기에 남발은 좋지 않다. 하지만, 임계영역은 반드시 보호해야 하므로 임계영역을 최대한 줄인다.

#### 올바른 종료 코드는 구현하기 어렵다.
영구적으로 돌아가는 시스템과 잠시 돌다 깔끔하게 종료하는 시스템은 구현하는 방법이 다르다. <br/>
깔끔하게 종료하는 코드는 올바로 구현하기가 어렵다. 절대 오지 않을 시그널을 기다리는 데드락 상태가 걸릴 수 있기 때문.

  **권장 사항** : 종료 코드를 개발 초기부터 고민하고 동작하게 초기부터 구현하라, 생각보다 오래 걸리고 어렵기에 이미 나온 알고리즘을 검토
  
#### 스레드 코드 테스트하기
코드가 올바르다고 증명하기는 현실적으로 불가능하다. 테스트가 정확성을 보장하지는 않지만, 충분한 테스트는 위험을 낮춘다.

1. 말이 안되는 실패는 잠정적인 스레드 문제로 취급하라
다중 스레드 코드는 때때로 말이 안되는 오류를 일으킨다. 이 일회성 문제를 계속 무시한다면 잘못된 코드 위에 코드가 쌓인다.

2. 다중 스레드를 고려하지 않은 순차 코드부터 제대로 돌게 만들자
스레드 환경 밖에서 생기는 버그와 스레드 환경에서 생기는 버그를 동시에 디버깅하지 마라. 먼저 스레드 환경 밖에서 코드를 올바로 돌려라.

3. 다중 스레드를 쓰는 코드 부분을 다양한 환경에 쉽게 끼워 넣을 수 있게 스레드 코드를 구현하라
한 스레드로 실행, 다중으로 실행, 실행 중 스레드 수 변경, 환경 변경, 다양한 속도 등.

4. 다중스레드를 쓰는 코드 부분을 상황에 맞게 조율할 수 있게 작성해라
적절한 스레드 개수를 파악할면 상당한 시행착오가 필요. 프로그램 처리율과 효율에 따라 스스로 스레드 개수를 조율하는 코드도 고민

5. 프로세서 수보다 많은 스레드를 돌려보라
스와핑을 일으키려면 프로세서 수보다 많은 스레드를 돌려야 하고, 스와핑이 잦으면 문제를 일으키는 코드를 찾기 쉬워진다.

6. 다른 플렛폼에서 돌려보라
처음부터 그리고 자주 모든 목표 플랫폼에서 코드를 돌려라

7. 코드에 보조 코드를 넣어 돌려라. 강제로 실패를 일으키게 해보라
보조 코드를 추가하는 방법은 두 가지 (직접 구현하기, 자동화) 이다. 흔들기 기법을 사용해 오류를 찾아내보자

#### 사견을 덧붙이면...?
어렵다! 이 한 마디로 표현이 가능할 것 같다. <br/>
처음 자바를 공부할 때도 이 부분이 어려웠고, 현업 개발자인 지금도 스레드 관련 부분은 어렵다. <br/>
물론 개념은 알고 있다. 하지만 항상 그렇듯 이론과 실제의 갭이랄까, 현업에서 스레드를 다뤄본 기억이 그렇게 있진 않다. <br/>
그렇기 때문에 지금도 어렵다고 생각하는 것이고, 이번의 동시성 얘기도 아, 그렇구나 하는 정도로 읽었다. <br/>
정리할 때는 어느 정도 이해를 바탕으로 정리를 하는데, 이번에는 내용도 길고 퇴근 후 짬짬히 읽고 정리하는 수준이라 이틀에 걸쳐 정리하였다. <br/>
그리고 이 스레드 라는게 면접 단골 질문이기도 해서, 추후에 멀티 스레드 및 테스트에 관한 글을 또 정리할 예정이다. <br/>

 
