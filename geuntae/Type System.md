## 널 가능성( Nullable )
널 가능성은 NPE( NullPointException )을 피하기 위한 코틀린 타입 시스템의 특성이다.
널이 될 수 있는지의 여부를 붙여줌으로써 컴파일러가 여러 가지 오류를 컴파일 시 미리 감지해서 실행 시점에 발생할 수 있는 예외 가능성을 줄일 수 있다.

![](https://velog.velcdn.com/images/dymnam/post/9b78eafa-daf4-4283-a5ce-00fd34950be9/image.png)

- 코틀린에서는 쉽게 타입 뒤에 ?를 붙임으로써 nullable하게 만들 수 있다.

## 안전한 호출 연산자: ?.
?. 은 null 검사와 메소드 호출을 한 번의 연산으로 수행한다.
```kotlin
//Null Safe 연산자를 사용해 간결하게 표현.
fun printAllCars(s: String?) {
    val allCars: String? = s?.toUpperCase()
    println(allCars)
}

fun main(args: Array<String>) {
    printAllCars("CarA")
    printAllCars(null)
    printAllCars("CarB")
}
```

## 엘비스 연산자: ?:
코틀린에서 null 대신 디폴트 값을 지정할 때 편리하게 사용할 수 있는 연산자인 ?: 를 지원한다.

코틀린에서는 return이나 throw 등의 연산도 식으로 분류해 엘비스 연산자의 유형에 return, throw 등의 연산을 넣을 수 있다.

```kotlin
fun elvis(s: String?) {
    // t가 null이면 결과는 elvis Type 임.
    val t: String = s ?: "elvis Type"
    println(t)
}

fun main(args: Array<String>) {
    elvis(null)
    elvis("abc")
}
```

## 안전한 캐스트: as?
as?는 값을 대상 타입으로 변환( 캐스팅 )할 수 없으면 null을 반환한다.
![](https://velog.velcdn.com/images/dymnam/post/d185041b-8597-432c-a748-868b4771aef5/image.png)

```kotlin
// 안전한 캐스트 연산자를 이용한 equals 구현 패턴
// 보통 안전한 캐스트를 사용할 때, 뒤에 엘비스 연산자를 사용하는 패턴을 자주 사용한다.

class SafePerson(val firstName: String, val lastName: String) {
    override fun equals(other: Any?): Boolean {
        val otherPerson = other as? SafePerson ?: return false

        return otherPerson.firstName == firstName &&
                otherPerson.lastName == lastName
    }

    override fun hashCode(): Int =
         super.hashCode() * 37 + lastName.hashCode()
}

fun main(args: Array<String>) {
    val p1 = SafePerson("Dmitry", "Jemerov")
    val p2 = SafePerson("Dmitry", "Jemerov")
    println(p1 == p2)
    println(p1.equals(42))
}
```
위 패턴을 사용하면 파라미터로 받은 값이 원하는 타입인지 쉽게 검사하고 캐스트할 수 있으며, 타입이 맞지 않으면 false를 반환한다.

## 널 아님 단언: !!
!! 를 사용하면 어떤 값이든 널이 될 수 있는 타입으로 바꿀 수 있다.( 강제성 )
실제 널에 대해 !! 를 사용하면 NPE가 발생한다.
```kotlin
fun ignoreNulls(s: String) {
    val sNotNull: String = s!!
    println(sNotNull.length)
}
```

## let 함수
let 함수를 사용하면 널이 될 수 있는 식을 쉽게 다룰 수 있다.
?. <- 안전한 호출 연산자와 함께 사용하여 결과가 널인지 검사한 다음에 그 결과를 변수에 대입하는 작업으로 간단하게 식을 만들 수 있다.
```kotlin
// let과 안전연산자 ?.dmf 사용해 null 객체를 다룰 때 좀 더 간결해지는 예제이다.
fun sendEmailTo(email: String) {
    println("Sending email to $email") // $는 받은 email 정보를 가져옴
}

fun main(args: Array<String>) {
    var email: String? = "ex@email.com" // ?를 붙이면서 nullable 함을 알림
    // email이 null이 아닐 경우, let의 람다로 전달되어 sendEmailTo 함수가 호출된다.
    email?.let { sendEmailTo(it) } // it == email
}
```

## 나중 초기화 lateinit
객체 인스턴스를 생성한 뒤 나중에 초기화하는 프레임워크가 많은데, 코틀린에서는 클래스 내에 존재하는 널이 될 수 없는 프로퍼티를 생성자 안에서 초기화하지 않고 특별한 메소드 안에서 초기화 할 수 없다.
그렇기 때문에, lateinit 이라는 변경자를 지원한다.
```kotlin
class LateinitEx {
    fun performAction(): String = "foo"
}
// lateinit을 사용해 늦은 초기화를 할 수 있다.
class MyTest {
    private lateinit var myLateinitEx: LateinitEx
    
    @Before
    fun setUp() {
        myLateinitEx = LateinitEx()
    }
    
    @Test
    fun testAction() {
        myLateinitEx.performAction()
    }
}
```
> lateinit 프로퍼티는 항상 var 로 선언해야하며, 초기화 하기 전에 접근하면 has not been initialized 예외가 발생한다.

## 코틀린의 원시 타입
#### 원시 타입: Int, Boolean 등
원시 타입의 변수에는 그 값이 직접 들어가지만, 참조 타입의 변수에는 메모리상의 객체 위치가 들어간다.
자바는 참조 타입이 필요한 경우 특별한 래퍼 타입( Integer 등 )으로 원시 타입 값을 감싸서 사용한다.
코틀린은 원시 타입과 래퍼 타입을 구분하지 않으므로 항상 같은 타입을 사용한다.
```kotlin
fun showProgress(progress: Int) {
    val percent = progress.coerceIn(0, 25)
    println("We're ${percent}% done!")
}

//fun main(args: Array<String>) {
//    var value: Int = 120
//    showProgress(value)
//}
```
코틀린에서는 실행 시점에 숫자 타입이 가장 효율적인 방식으로 표현된다.
대부분의 경우 코틀린의 Int는 자바의 int 타입으로 컴파일 된다.

#### 자바의 원시 타입
- 정수 타입 : Byte, Short, Int, Long
- 부동소수점 타입 : Float, Double
- 문자 타입 : Char
- 불리언 타입 : Boolean

## 널이 될 수 있는 원시 타입: Int?, Boolean? 등
이미 알고 있듯 null은 자바의 잠조 타입의 변수에만 대입할 수 있다.
그렇기에 null이 될 수 있는 코틀린 타입은 자바 원시 타입으로 표현할 수 없다.
따라서 코틀린에서 널이 될 수 있는 원시 타입을 사용하면 그 타입은 자바의 래퍼 타입으로 컴파일된다.
```kotlin
data class Person(val name: String, val age: Int? = null) {
    fun isOlderThan(other: Person): Boolean? {
        if (age == null || other.age == null) {
            return null
        }
        return age > other.age
    }
}

fun main(args: Array<String>) {
    println(Person("Sam",35).isOlderThan(Person("Amy", 24))) // true
    println(Person("Sam",35).isOlderThan(Person("Jane"))) // null
}
```
Person 클래스에 선언된 age는 null을 저장했기 때문에 자바의 Integer로 저장된다.

## 숫자 변환
코틀린과 자바의 가장 큰 차이점 중 하나는 숫자를 변환하는 방식이다.
코틀린은 한 타입의 숫자를 다른 타입의 숫자로 자동 변환하지 않는다.
결과 타입이 허용하는 숫자의 범위가 원래 타입의 범위보다 넓은 경우 조차도 자동 변환은 불가능하다.
때문에, 코틀린에서 모든 원시 타입에 대한 변환 함수를 제공한다
#### 변환 함수의 이름 예제
- toByte()
- toShort()
- toChar()
- toLong()
*추가적 예외* toInt() -> 표현 범위가 더 좁은 타입으로 변환하면 일부를 잘라냄.

```kotlin
fun main(args: Array<String>) {
    val i= 1.423
    val s: Short = i.toInt().toShort()
    println(s)
}
```

## 최상위 타입: Any, Any?
자바에서 Object가 클래스 계층의 최상위 타입이듯이 코틀린에서는 Any 타입이 모든 널이 될 수 없는 타입의 조상이다.
코틀린에서는 Any가 Int 등의 원시 타입을 포함한 모든 타입의 조상 타입이다.
```Kotlin
    val answer: Any = 24 // Any가 참조 타입이어서 24가 박싱된다.

```

## Unit 타입 : 코틀린의 void
코틀린의 Unit은 자바의  void와 같은 기능을 한다.
Unit은 모든 기능을 갖는 일반적인 타입이며, void와 달리 Unit을 타입 인자로 쓸 수 있다는 특징을 가지고 있다.

Unit 타입에 속한 값은 단 하나뿐이며, 이름도 Unit이다.
Unit 타입 함수는 Unit 값을 묵시적으로 반환한다.
-> 두 특성은 **제네릭 파라미터를 반환하는 함수를 오버라이드**하면서 반환 타입으로 Unit을 쓸 때 유용하다.

```kotlin
interface Processor<T> {
    fun process(): T
}

class NoResultProcessor: Processor<Unit> {
    override fun process() { // Unit을 반환하지만 타입을 저장할 필요는 없음.
        TODO("Not yet implemented")
        // Unit == Void, return을 명시 할 필요가 없다.
    }
}
```

## Nothing 타입 : 이 함수는 결코 정상적으로 끝나지 않는다.
코틀린에는 결코 성공적으로 값을 돌려주는 일이 없어서 '반환 값'이라는 개념 자체가 의미 없는 함수가 **일부 존재**한다.
Nothing 타입은 아무 값도 포함하지 않아서 함수의 반환 타입이나 그 값으로 쓰일 타입 파라미터만 쓸 수 있다.
컴파일러는 Nothing이 반환 타입인 함수가 결코 정상적으로 종료되지 않음을 알고 그 함수를 호출하는 코드 분석 시 사용한다.

- Nothing은 어떤 값도 포함하지 않는 타입으로 private constructor로 정의되어 있어 인스턴스를 생성할 수 없다.

```kotlin
fun fail(message: String): Nothing {
    throw IllegalStateException(message)
}
```

#### *추가* dispatch
디스패치는 객체지향 언어에서 동적 타입에 따라 적절한 메소드를 호출해주는 것을 동적 디스패치라고한다.
컴파일 시점에 결정하여 코드를 생성하는 방법을 정적 디스패치라고 한다.
보통 동적 디스패치는 객체 별로 자신의 메소드에 대한 테이블을 저장하는 방법을 많이 사용한다.
