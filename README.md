# Kotlin-Study

## Reactive Programming

## JVM

## Kotlin이란 ?

## Kotlin 버전 별 정리

## 안드로이드 생명주기

## 코틀린 타입 시스템
#### Null 가능성
안전한 호출 연산자: "?."
엘비스 연산자 "?:"
안전한 캐스트: as?
널 아님 단언: !!
let함수
나중에 초기화할 프로퍼티
널이 될 수 있는 타입 확장
타입 파라미터의 널 가능성

#### 코틀린 기본 타입
기본 타입: Int, Boolean 등
널이 될 수 있는 기본 타입: Int?, Boolean? 등
Any, Any?: 최상위 타입
Unit 타입: 코틀린의 void
Nothing 타입: “이 함수는 결코 정상적으로 끝나지 않는다.”

## 함수
함수
확장 함수
infix 함수
스코프 함수

## 배열
Array
List
ArrayList

## 반복문
for
while

## 제어문
if ~ else
when( 자바의 Switch 문 )과 enum

## 코틀린의 예외 처리
try, catch, finally

## 상속

## 클래스, 객체, 인터페이스
#### 클래스 계층 정의
코틀린 인터페이스
open, final, abstract 변경자: 기본적으로 final
가시성 변경자: 기본적으로 공개
내부 클래스와 중첩된 클래스: 기본적으로 중첩 클래스

#### 뻔하지 않은 생성자와 프로퍼티를 갖는 클래스 선언
클래스 초기화: 주 생성자와 초기화 블록
부 생성자: 상위 클래스를 다른 방식으로 초기화
인터페이스에 선언된 프로퍼티 구현

#### 컴파일러가 생성한 메소드: 데이터 클래스와 클래스 위임
모든 클래스가 정의해야 하는 메소드
데이터 클래스: 모든 클래스가 정의해야 하는 메소드 자동 생성
클래스 위임: by 키워드 사용

#### object 키워드: 클래스 선언과 인스턴스 생성
객체 선언: 싱글턴을 쉽게 만들기
동반 객체: 팩터리 메소드와 정적 멤버가 들어갈 장소
동반 객체를 일반 객체처럼 사용

## 람다로 프로그래밍
#### 람다 식과 멤버 참조
람다 소개: 코드 블록을 함수 인자로 넘기기
람다와 컬렉션
람다 식의 문법
현재 영역에 있는 변수에 접근
멤버 참조

#### 컬렉션 함수형 API
필수적인 함수: filter와 map
all, any, count, find: 컬렉션에 술어 적용
groupBy: 리스트를 여러 그룹으로 이뤄진 맵으로 변경
flatMap과 flatten: 중첩된 컬렉션 안의 원소 처리

#### 지연 계산 lazy 컬렉션 연산
시퀀스 연산 실행: 중간 연산과 최종 연산
시퀀스 만들기

#### 수신 객체 지정 람다: with와 apply
with함수
apply함수

## 코틀린의 Collection
널 가능성과 컬렉션
읽기 전용과 변경 가능한 컬렉션

## 연산자 오버로딩과 관례
#### 산술 연산자 오버로드
이항 산술 연산 오버로딩
복합 대입 연산자 오버로딩
단항 연산자 오버로딩

#### 비교 연산자 오버로딩
동등성 연산자: "equals"
순서 연산자: compareTo

#### 관례
in관례
rangeTo관례
for 루프를 위한 iterator 관례

#### 구조 분해 선언과 component 함수
구조 분해 선언과 루프

#### 프로퍼티 접근자 로직 재활용: 위임 프로퍼티
위임 프로퍼티 사용: by lazy()를 사용한 프로퍼티 초기화 지연
위임 프로퍼티 구현
위임 프로퍼티 컴파일 규칙
프로퍼티 값을 맵에 저장
프레임워크에서 위임 프로퍼티 활용

## 고차 함수: 파라미터와 반환 값으로 람다 사용
#### 고차 함수 정의
함수 타입
인자로 받은 함수 호출
디폴트 값을 지정한 함수 타입 파라미터나 널이 될 수 있는 함수 타입 파라미터
함수를 함수에서 반환
람다를 활용한 중복 제거

#### 인라인 함수: 람다의 부가 비용 없애기
인라이닝이 작동하는 방식
인라인 함수의 한계
컬렉션 연산 인라이닝
함수를 인라인으로 선언해야 하는 경우
자원 관리를 위해 인라인된 람다 사용

#### 고차 함수 안에서 흐름 제어
람다 안의 return문: 람다를 둘러싼 함수로부터 반환
람다로부터 반환: 레이블을 사용한 return
무명 함수: 기본적으로 로컬 return

## 제너릭 Generics
#### 제네릭 타입 파라미터
제네릭 함수와 프로퍼티
제네릭 클래스 선언
타입 파라미터 제약
타입 파라미터를 널이 될 수 없는 타입으로 한정

#### 실행 시 제네릭스의 동작: 소거된 타입 파라미터와 실체화된 타입 파라미터
실행 시점의 제네릭: 타입 검사와 캐스트
실체화한 타입 파라미터를 사용한 함수 선언
실체화한 타입 파라미터로 클래스 참조 대신
실체화한 타입 파라미터의 제약

#### 변성: 제네릭과 하위 타입
변성이 있는 이유: 인자를 함수에 넘기기
클래스, 타입, 하위 타입
공변성: 하위 타입 관계를 유지
반공변성: 뒤집힌 하위 타입 관계
사용 지점 변성: 타입이 언급되는 지점에서 변성 지정
스타 프로젝션: 타입 인자 대신 * 사용

## 애노테이션과 리플렉션
#### 애노테이션 선언과 적용
애노테이션을 활용한 JSON 직렬화 제어
애노테이션 선언
메타애노테이션: 애노테이션을 처리하는 방법 제어

#### 리플렉션: 실행 시점에 코틀린 객체 내부 관찰
코틀린 리플렉션 API: KClass, KCallable, KFunction, KProperty
리플렉션을 사용한 객체 직렬화 구현
애노테이션을 활용한 직렬화 제어
JSON 파싱과 객체 역직렬화
최종 역직렬화 단계: callBy(), 리플렉션을 사용해 객체 만들기

## 디자인 패턴
MVC
MVP
MVVM
옵저버
싱글톤
어댑터

## 코루틴 Coroutine

## Data Class

## InLine Function

## Diff Util

## Room Database
