## JVM
JVM은 Java Virtual Machine의 줄임말로, 자바 애플리케이션을 클래스 로더를 통해 읽어들여 API와 함께 실행하는 것이다.
JVM은 Java와 OS사이에서 중개자 역할을 수행하여 Java가 OS에 구애받지 않고 재사용 가능하게 해준다.
또한, 메모리관리, Garbage Collection을 수행하며, 스택기반의 가상머신이다.

## JVM을 알아야 하는 이유
동일한 기능의 프로그램이더라도 메모리 관리에 따라 성능이 좌우되는데, JVM은 한정된 메모리를 효율적으로 사용하여 최고의 성능을 낼 수 있게 도와준다.
메모리가 관리되지 않는 경우 속도저하 현상이나 튕김 현상이 생길 수 있다.
덧붙여 자바는 완전한 기계어가 아니라 바이트 코드이기 때문에 이것을 해석하고 실행할 수 있는 가상 운영체제가 필요하기 때문이다.

## JVM 흐름도
![](https://velog.velcdn.com/images/dymnam/post/655366c1-a38b-46f9-bc0f-f0ca83ad0045/image.png)
1. 프로그램이 실행되면 JVM은 OS로부터 해당 프로그램이 필요로하는 메모리를 할당받는다.
2. 자바 컴파일러( javac )가 자바 소스코드( .java )를 읽어들여 자바 바이트코드( .class )로 변환시킨다.
3. Class Loader를 통해 Class파일들을 JVM으로 로딩한다.
4. 로딩된 Class파일들은 Execution Engine을 통해 해석된다.
5. 해석된 바이트코드는 Runtime Data Areas에 배치되어 실질적인 수행이 이루어진다.

이러한 실행과적 속에서 JVM은 필요에 따라 Thread Synchronization과 GC같은 관리작업을 수행한다.

## JVM 구성
#### Class Loader( 클래스 로더 )
JVM 내로 클래스( .class )파일을 로드하고, 링크를 통해 배치하는 작업을 수행하는 모듈이다.
Runtime 시에 동적으로 클래스를 로드한다.
.jar 파일 내 저장된 클래스들을 JVM위에 탑재하고 사용하지 않는 클래스들은 메모리에서 삭제한다.
자바는 컴파일 타임이 아니라 런타임에 참조한다.

#### Execution Engine( 실행 엔진 )
클래스를 실행시키는 역할로, 클래스 로더가 JVM 내의 런타임 데이터 영역에 바이트 코드를 배치시키고, 배치된 코드는 실행 엔진에 의해 실행된다.
자바 바이트코드는 기계가 바로 수행할 수 있는 언어보다는 비교적 인간이 보기 편한 형태로 기술된 것이다.

실행 엔진은 바이트코드를 실제로 JVM 내부에서 기계가 실행할 수 있는 형태로 변경하는데, 이 방법은 두 가지가 있다.
- Interpreter( 인터프리터 ) : 실행 엔진은 자바 바이트 코드를 명령어 단위로 읽어서 실행한다. 이 방식은 인터프리터 언어의 단점을 그대로 갖고 있어 한 줄 씩 수행하는 이유로 느리다.

- JIT( Just - In - TIme ) : 인터프리터 방식의 단점을 보완하기 위해 도입된 JIT 컴파일러로, 인터프리터 방식으로 실행하다가 적절한 시점에 바이트코드 전체를 컴파일하여 네이티브 코드로 변경한다.
네이티브 코드는 캐시에 보관하기 때문에 한 번 컴파일 된 코드는 빠르게 수행된다.

#### Garbage Collector
GC를 수행하는 모듈( Thread )이 있다.
