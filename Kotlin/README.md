출처 : [디모의 Kotlin 강좌](https://www.youtube.com/playlist?list=PLQdnHjXZyYadiw5aV3p6DwUdXV2bZuhlN)   
       **Do it! 코틀린 프로그래밍**
       
       앞부분도 7강 이후처럼 수정필요


「Kotlin」
=============

> 자료형 오류를 미리 잡을 수 있는 '정적 언어'   
> NullSafe   
> 간결하고 효율적   
> 함수형 프로그래밍, 객체 지향 프로그래밍 모두 가능   
> 세미콜론을 생략할 수 있음;

# 코틀린 패키지
> _프로젝트는 모듈⊃패키지⊃파일 로 구성_   

* 패키지 이름을 선언하지 않으면 그 파일은 자동으로 default 패키지에 포함   
* `import`로 다른 패키지 사용할 수 있음   
* 이 파일과 패키지 내에 같은 이름의 클래스가 있다면 `import ~~ as ~~` 로 별명을 지어서 사용   

코틀린의 자료형은 **참조형 자료형** _성능 최적화를 위해 코틀린 컴파일러에서 다시 기본형으로 대체되므로 이러한 최적화를 내가 신경쓰지 않아도 됨_   
값(동등성) 비교 `==`   
참조 비교 `===`   
자료형 검사 `is`   
스마트 캐스트 자료형 `Number` , `Any` (`Any`는 최상위 기본 클래스)

## 자료형에 별명 붙이기
> `typealias` 이용해 자료형에 별명 붙임. 고차 함수와 람다식에서 많이 씀.

	typealias Username = String
	val user: Username = "Kildong"

# 21~~~
* ?. !!. ?: 엘비스연산자

# 210112
* 함수
* 간단하게 표현한 함수
* 반환값이 없는 함수(`Unit` 자료형, `Unit` 과 `void` 의 차이점)
* 매개변수의 기본값
* 매개변수 이름과 함께 함수 호출
* 가변인자 vararg
* 순수함수
* 람다식, 일급객체(일급객체는 1.함수의 인자로 전달할 수 있음 2.함수의 반환값에 사용할 수 있음 3.변수에 담을 수 있음)
* 고차함수
* 함수형 프로그래밍의 정의와 특징(1.순수 함수를 사용해야 함 2.람다식을 사용할 수 있음 3.고차 함수를 사용할 수 있음)
* nestedLambda

# 210114
* call by value 와 call by name 의 차이
* 함수 이름 앞에 `::` 기호를 사용해 소괄호 와 인자를 생략하고 람다식과 같이 사용 가능?
* `::` 는 함수 참조 기호. (128페이지 헷갈린다)
* 람다식의 매개변수 개수에 따라 람다식을 구성하는 방법 128p ~
* 람다식의 특정 매개변수를 사용하지 않을때에는 언더스코어 `_` 로 대체하면 됨
* 일반 매개변수와 람다식 매개변수를 함께 사용할 때 람다식 매개변수가 마지막 인자 위치에 있으면 소괄호 바깥으로 뺄 수 있다.
	> `sumFunc("aa","bb",{a,b->"$a $b"})` -> `sumFunc("aa","bb"){a,b->"$a $b"}`

# 210116
* 익명 함수 : 함수 본문 조건식에 따라 함수를 중단하고 반환해야 하는 경우
* 인라인 함수 : 함수가 호출되는 곳에 함수 본문의 내용을 모두 복사해 넣어 함수의 **분기** 없이 처리되기 때문에 코드의 성능을 높일 수 있음
	> `inline` , `noninline` , `crossinline` -> 코드작성단계에서 오류를 보여줘 잘못된 비지역 반환을 방지할 수 있음

# 210119 꼬리재귀함수 어렵다
* 확장 함수 : 클래스처럼 필요로 하는 대상에 함수를 더 추가 할 수 있음
* 중위 함수 : 일종의 연산자를 구현할 수 있는 함수 (`3.multiply(10)` 이 아닌 infix func은 `3 multiply 10`)
	> 중위 함수 조건 : 1.멤버 메서드 또는 확장 함수여야 함 2.하나의 매개변수를 가져야 함 3.infix 키워드를 사용하여 정의
* 꼬리 재귀 함수 : 일반적인 재귀에서는 재귀 함수가 먼저 호출되고 계산, 꼬리 재귀는 계산을 먼저하고 재귀함수가 호출 **tailrec** 키워드 사용
	> 재귀 함수의 스택 오버플로 현상을 해결 -> 스택 메모리 안정성   
	> `return n * factorial(n-1)` 이 아닌 `return factorial(n-1, run*n)` 이런식으로 계산하고 호출, 따라서 스택 메모리 낭비 X   
	> `tailrec` 키워드를 붙이지 않으면 내부적으로(바이트코드로 확인했을 때) 재귀함수로 되어있다. 컴파일러가 임의로 루프코드로 변환하지 않는듯.   
	> `tailrec` 키워드를 붙여야 컴파일러에서 재귀가 아닌 루프로 변환하여 실행하므로 스택메모리 낭비가 없다.
* 최상위 함수와 지역함수, 지역 변수와 전역 변수

# 210120
* 조건문
* `in` 연산자와 범위 연산자 `..`
* 조건이 많을때의 `when`
	> switch case와 유사하나 break 불필요   
	> 함수의 반환값과도 비교 가능   
	> in 연산자와 범위연산자 사용 가능   
	> is 키워드를 사용해 특정 자료형을 검사 가능   
	> 인자가 없는 when문도 있음 -> 인자 있는 when문과 다르게 조건식을 구성할 수 있음 (>,<,<= 등등)

* 반복문
	> `in` 연산자와 범위연산자 활용   
	> 하행은 `downTo`   
	> 증감값 설정 `step`

## 흐름의 중단과 반환 p.179
* 람다식에서 return 사용하기 : 인라인으로 선언되지 않은 람다식에서는 `return@label` 과 같이 레이블 활용.
	> 암묵적 레이블 : 람다식 표현식 블록에 직접 라벨을 쓰는 것이 아닌 람다식의 명칭을 그대로 라벨처럼 사용.   
* 예외처리,발생,사용자정의 예외
	> `try` `catch` `finally` `throw`
* 정규식 : matches와 Regex (https://regexr.com/ 에서 연습가능)

# 210122 클래스 시작
* 클래스, 생성자, 상속
	> 
	> `constructor`, 프로퍼티와 함께, `init{}`, `open`

# 210126
* 다형성
	> 매개변수가 서로 다른 형태를 취하거나, 실행 결과를 다르게 가질 수 있는 것   
	> 오버로딩(Overloading) : 동작은 동일하지만 인자의 형식만 달라지는 것   
	> 오버라이딩(Overriding) : 상위와 하위 클래스에서 메서드나 프로퍼티의 이름은 같지만 기존의 동작을 다른 동작으로 재정의하는 것   
	> 기반클래스에 `open`, 파생클래스에 `override` 키워드 사용. 코틀린은 메서드 뿐만 아니라 프로퍼티도 오버라이딩(재정의) 가능   
	> 오버라이딩을 막으려면 `final` 키워드   
* super 와 this
* 이너 클래스에서 바깥 클래스 호출하기
	> `super` 키워드와 함께 @ 기호옆에 바깥 클래스 이름을 작성. eg.`super@Child.f()` -> **현재 이너 클래스의 바로 바깥 클래스인 Child의 상위클래스에 접근**   
* 인터페이스에서 참조하기
	> 앵글 브래킷 `<>`을 사용해 접근하려는 클래스나 인터페읏의 이름을 정해줌. eg. `super<A>.f()` , `super<B>.f()`

# 210128
* 정보 은닉 캡슐화
	> private(-), public(+), protected(#), internal(아직없음)   
	> 오버라이딩된 멤버는 상위클래스와 동일한 가시성 지시자를 갖음
* 클래스와 클래스의 관계
	> 연관, 의존, 집합, 구성 그리고 각각의 생명주기 의존성

# 210203 프로퍼티와 초기화
* 코틀린은 Getter와 Setter가 자동생성
* 커스텀 Getter와 Setter
	> `value` : 세터의 매개벼수로 외부로부터의 값을 가져옴. 이름변경 가능   
	> 보조필드 `field` : 프로퍼티를 참조하는 변수. 이름변경 불가   
	> `private set` : 외부에서 객체 생성 후 값을 재할당하는 것 금지
* 보조 프로퍼티
* 지연 초기화와 위임
	> 객체의 정보가 나중에 나타나는 경우 객체 생성과 동시에 초기화 하기 힘든 경우   
	> `lateinit` , `lazy`   
	> `lateinit` 지연 초기화 : 1.특정 객체의 의존성이 있는 경우 2.유닛 테스트를 할 때 임시적으로 객체를 생성시켜야 하는 경우   
	> `lateinit` 은 `var`로 선언된 프로퍼티에만 사용할 수 있다. 프로퍼티에 대한 Getter와 Setter를 사용할 수 없다.   
	> 프로퍼티 지연 초기화 말고도 객체 지연 초기화에도 사용 가능.   
	> `lateinit var person1 : Person` --나중에-> `person1 = Person("둘리",3)`
	
	> `lazy` 는 불변의 변수인 `val`에서만 사용 가능.(읽기전용) `val something by lazy{...}` 라는 식으로 사용. (`by`는 프로퍼티를 위임할 때 사용하는 키워드)   
	> `lazy` 는 **람다식**으로 구성되어 lazy 인스턴스 반환값을 가지는 **함수** (마지막줄이 반환값)   
	> `lazy` 의 핵심은 프로퍼티에 **최초**로 접근한 시점에 해당 프로퍼티가 초기화   
	> 프로퍼티 지연 초기화 말고도 객체 지연 초기화에도 사용 가능.   
	> `val person : Person by lazy {...}` or **위임변수**를 사용-> `val personDelegate = lazy{ Person("또치",3) }`   
* `by lazy`와 `lazy`의 차이점
	> `by lazy`는 객체의 위임을 나타냄   
	> `lazy`는 변수에 위임된 **`Lazy` 객체 자체**를 나타냄. p.271
* p.272에 lazy 선언부 확인 가능
* `isInitialized` : 프로퍼티가 초기화되었는지 검사하는 코틀린 표준 함수의 API.
* 프로퍼티 참조를 위해 콜론 2개(::) 사용. p.267

## 위임? Delegate? 뭐지? p.270


# 210211 프로퍼티와 초기화
	> 코틀린의 프로퍼티 = 필드(변수) + Getter 와 Setter

* `by`를 통한 위임
	> `<val|var|class> 프로퍼티 혹은 클래스 이름 : 자료형 by 위임자`   
	> 상속과 비슷하게 해당 클래스의 모든 기능을 사용하면서 동시에 기능을 추가 확장 구현   
	> 클래스의 위임 : 특정 참조 없이 메서드 호출 가능   
	> 프로퍼티 위임 : 해당 객체를 접근하는 시점에서 초기화 -> 시작할 때마다 프로퍼티를 생성하느라 소비되는 시간 감소
* `observable()` `vetoable()`
	> `import kotlin.properties.Delegates`   
	> `observable()` : 프로퍼티를 감시하고 있다가 변경이 일어날 때 호출되어 처리 -> **콜백**이라고 함   
	> `vetoable()` : `observable()`과 비슷, 반환값에 따라 프로퍼티 변경을 허용하거나 취소 가능   
	> `vetoable()` 함수는 컬렉션과 같이 큰 데이터를 다룰 때 유용
* 정적 변수와 컴패니언 객체
	> 인스턴스화할 필요 없이 사용, 모든 객체에 의해 공유되는 효과   
	> `companion object`   
	> **싱글톤**으로 정의   
	> **싱글톤** : 전역 변수를 사용하지 않고 객체를 하나만 생성하도록 하며, 생성된 객체를 어디에서든지 참조할 수 있도록 하는 디자인 패턴의 하나   
* 애노테이션
	> `@JvmStatic` , `@JvmField`
* 최상위 함수(패키지 레벨 함수)
	> 자바에서 코틀린의 최상위 함수에 접근할 때 자동 생성된 클래스의 멤버 메서드처럼 접근할 수 있음   
	> 자동 생성된 클래스의 이름은 "파일 이름 + 확장자 이름" 으로 되어있음   
	> `@file:JvamName("설정하는 이름")` 으로 자동 생성될 클래스의 이름을 정해줄 수 있음   
* object와 싱글톤
* object 선언
	> 멤버 프로퍼티와 메서드를 객체 생성 없이 이름의 점(`.`) 표기법으로 바로 사용 가능   
	> 단일 인스턴스를 생성해 처리하기 때문에 싱글톤 패턴에 이용   
	> 접근 시점에 객체가 생성 -> 생성자 호출 X -> 주 생성자, 부 생성자 사용 X   
	> 초기화 블록인 `init`은 들어갈 수 있는데 최초 접근에서 실행   
	> 클래스나 인터페이스를 상속할 수 있음   
	> 자바에서는 `이름.INSTANCE`로 접근   
* object 표현식
	> 싱글톤 아님   
	> 이름이 없는 익명 내부 클래스로 불리는 형태를 object 표현식으로 만들 수 있음   
	> 하위 클래스를 만들지 않고도 클래스의 특정 메서드를 **오버라이딩**   
	> 자바의 익명 내부 클래스와 같이, object 표현식 안의 코드는 둘러싸여 있는 범위 내부의 변수에 접근 가능

# 210211 7장 다양한 클래스와 인터페이스
	> 7-1 추상 클래스와 인터페이스

* 추상클래스와 인터페이스의 공통점과 차이점
	> 공통점 : 하위에서 더 자세히 구현하는 구체화 필요   
	> 차이점 : 인터페이스에서는 프로퍼티에 상태 정보를 저장할 수 없음   
	> 차이점 : 인터페이스에서는 다중 상속과 같이 여러 개의 인터페이스를 하나의 클래스에서 구현하는 것 가능   
* 추상 클래스
	> `abstract class Vehicle` 처럼 `abstract` 키워드 사용   
	> 기본 설계 역할   
	> 추상 프로퍼티나 추상 메서드도 선언될 수 있음   
	> 일반 프로퍼티도 선언 가능하고 초깃값인 상태를 저장할 수 있음(인터페이스와의 차이점)   
	> `open` 키워드 없이도 재정의 가능   
	> 단일 인스턴스로 객체를 생성하려면 `object` 표현식 사용! (object로 딱 한번 구현한 뒤 사용)
* 인터페이스
	> 다른 객체 지향 언어와는 다르게 메서드에 구현 내용이 포함될 수 있음 -> 자바 인터페이스에서 `default` 키워드와 같음   
	> 하위 클래스는 상속을 하나만 허용, 하위 클래스는 상위 클래스와 강한 연관이 생기면서 영향을 받음 -> 인터페이스로 해결   
	> 하위 클래스 대신 **구현 클래스** 라고 함   
	> 메서드는 추상, 일반 모두 선언 가능. BUT 프로퍼티는 오직 추상 프로퍼티만 가능   
	> 추상 클래스와는 다르게 `abstract` 키워드를 붙이지 않아도 기본적으로 추상 프로퍼티, 추상 메서드   
* 인터페이스에서 `val`로 선언된 프로퍼티는 Getter를 통해 필요한 내용을 구현할 수 있음 p.305
	> 초기화할 수 없지만 Getter를 통해 반환값을 지정할 수 있음   
	> 하지만 여전히 보조 필드인 `field` 사용 불가   
	> `var`로 프로퍼티를 선언하더라도 보조 필드를 사용할 수 없기 때문에 `value`를 저장할 수 없음   
* 여러 인터페이스의 구현
	> `super<인터페이스이름>.메서드이름()` 형태로 이름이 동일한 경우 구분   
# 인터페이스의 위임 p.311 확실히 이해할 것
	
	
# 210212
	> 7-2 데이터 클래스와 기타 클래스
* 데이터(Data) 클래스, 실드(Sealed) 클래스, 이너(Inner) 클래스, 열거형(Enum) 클래스 등

## 데이터 클래스
	> `data` 키워드를 통해 선언   
	> 데이터 클래스 3가지 조건
* DTO(Data Transfer Object) : 데이터 전달을 위한 객체 (자바에서는 POJO(Plain Old Java Object)라고 부르기도 했음)   
* DTO는 구현 로직을 가지고 있지 않고 순수한 데이터 객체를 표현 -> 속성과 속성을 접근하고자 하는 Getter/Setter를 가짐   
* 추가적으로 `toString()`,`equals()` 등과 같은 데이터를 표현하거나 비교하는 메서드를 가져야 함   
* 코틀리에서는 Getter/Setter,`toString()`,`equals()`가 내부적으로 **자동 생성**   
* 코틀린 데이터클래스 자동생성 메서드 : Getter/Setter, `equals()`, `hashCode()`, `toString()`, `copy()`, `component1()`, `component2()` 등   
* 객체 디스트럭처링
	> `val (name,email) = cus1` -> 객체가 가지고 있는 프로퍼티를 개별 변수로 분해하여 할당   
	> 특정 프로퍼티를 가져올 필요가 없는 경우 언더스코어(`_`)를 사용해 제외. `val (_,email) = cus1`   
	> 개별적으로 가져올 때 사용하는 `componentN()`. `val name2 = cus1.component1()`   
	> `for((name,email) in customers)` customers 의 모든 객체를 반복하면서 프로퍼티를 분해   
	> `val (myName, myEmail) = myFunc()` 함수로부터 객체가 반환될 경우에도 사용 가능   
	> **람다식에서도 디스트럭처링 가능** p.321   
	
***
↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓
1. `equals()` : 내용의 동일성을 판단하는
2. `hashcode()` : 객체의 내용에서 고유한 코드를 생성하는
3. `toString()` : 포함된 속성을 보기쉽게 나타내는
4. `copy()` : 객체를 복사하여 똑같은 내용의 새 객체를 만드는
    똑같은 내용의 객체를 생성할 수 있지만 패러미터를 줘 일부 속성을 변경할 수도 있다.
    val a = Data("A",7)
    val b = a.copy()
    val c = a.copy("B")
5. `componentX()` : 속성을 순서대로 반환하는
    Data("A", 7) 에서 "A"가 component1(), 7이 component2()

## 예제
    fun main(){
        val a = General("A",1)
        println(a == General("A",1)
        println(a.hashcode())
        println(a)
        
        val b = Data("B",2)
        println(b == Data("B",2))
        println(b.hashcode())
        println(b)
        
        println(b.copy())
        println(b.copy("C"))
        println(b.copy(3))
    }
    class General(val name: String, val id: Int)
    data class Data(val name: String, val id: Int)


**for문의 내부적으로는 a에 component1(), b에 component2() 함수를 사용해 순서대로 값을 불러옴**

    fun main(){
        val list = listOf(Data("A",1),
                        Data("B",2),
                        Data("C",3))
        for((a,b) in list){    // 내부적으로는 a에는 component1()이 b에는 component2()라는 함수를 사용하여 순서대로 값을 불러옴
            println("${a}, ${b}")
        }
    }
    class General(val name: String, val id: Int)
↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑
***

## 내부 클래스 기법
> 중첩(Nested) 클래스   
> 이너(Inner) 클래스   
* 자바의 내부 클래스와의 비교
### 중첩 클래스
* 기본적으로 정적(static) 클래스처럼 다뤄짐
* 중첩클래스에서 바깥클래스의 멤버들에 접근은 안됨 -> Outer 클래스의 컴패니언 객체에는 접근 가능
### 이너 클래스
* 중첩클래스와는 다르게 바깥클래스의 멤버들에 접근 가능, 심지어 `private` 멤버도 접근 가능!
### 지역 클래스
* 특정 메서드의 블록이나 `init` 블록과 같이 블록 범위에서만 유효한 클래스
* 블록 범위를 벗어나면 더 이상 사용 X
### 익명 객체
* 특정 프로퍼티를 위해 일회성으로 사용
### 실드 클래스 (Sealed)
* 미리 만들어 놓은 자료형들을 묶어서 제공
1. 실드 클래스 그 자체는 추상 클래스와 같기 때문에 객체 생성 X
2. 생성자도 기본적으로는 `private`. `private` 이 아닌 생성자는 허용 X
3. 같은 파일 안에서는 상속이 가능, 다른 파일에서는 상속이 불가능하게 제한
4. 실드 클래스 블록 안에 선언되는 클래스는 상속이 필요한 경우 `open` 키워드로 선언될 수 있음
* 실드 클래스를 선언하는 두 가지 방법 1. 중괄호 사용 2. 중괄호 안사용 ㅋㅋ -> 이때는 내부 클래스를 상속할 때 점(`.`)표기로 접근하지 않고 내부 클래스 이름만 그대로 사용
* `when` 구문을 사용할 때 `else`문 사용할 필요 없다 -> 모든 경우를 열거? 실드클래스를 사용하면 필요한 경우의 수를 직접 지정할 수 있어서?
### 열거형 클래스
* 여러 개의 상수를 선언하고 열거된 값을 조건에 따라 선택할 수 있는 특수한 클래스
* 메서드를 포함할 수 있는데 세미콜론(`;`)을 사용해 열거한 상수 객체와 구분
* 기본 멤버들이 있음 (`name`, `ordinal`, `tostring()`, `values()` 등등)
### 애노테이션 클래스 - 모르겠다!
* 리플렉션
* 클래스 타입 `KClass<*>`
* 클래스 레퍼런스 표현 `클래스이름::class`

***
↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓
## 중첩클래스(Nested Class)
> _하나의 클래스가 다른 클래스의 기능과 강하게 연관되어 있다는 의미를 전달하기 위해 만들어진 형식_   
> _코드의 형태만 내부에 존재할 뿐 실질적으로는 서로 내용을 직접 공유할 수 없는 별개의 클래스_

    class Outer{
        class Nested{
        }
    }
    
사용할 때는 외부클래스이름.중첩클래스이름 `Outer.Nested()`   
이때 중첩클래스 대신 내부클래스라는 것을 사용할 수 있다.

## 내부클래스
> _혼자서 객체를 만들 수는 없고 외부 클래스의 객체가 있어야만 생성과 사용이 가능한 클래스_   
> _외부클래스 객체 안에서 사용되는 클래스 이므로 외부 클래스의 속성과 함수의 사용이 가능_

    class Outer{
        var text = "Outer Class"
        inner class Inner{
            var text = "Inner Class"
            fun introOuter(){
                println(this@Outer.text)    //외부클래스와 내부클래스에 같은 이름의 속성이나 함수가 있다면 외부클래스의 속성,함수는 'this@OuterClass이름' 으로 참조
            }
        }
    }

↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑
***

## 07-3 연산자 오버로딩
> p.340
* 연산자의 작동 방식
	> `val a = 5` `val b = 10` `print(a.plus(b))` 이는 `print(a+b)`와 동일
* operator 키워드
* `plus()` 연산자 오버로딩 예시
* `mod`연산자 함수 이름이 `rem` 으로 변경
### 호출 연산자
* `invoke`
### 대입 연산자
* `+`에 대응하는 `plus()`를 오버로딩하면 `+=` 는 자동으로 구현! -> 2개를 동시에 오버로딩하면 `+`의 동작을 무엇으로 할지 모호 -> 오류

# 08 제너릭과 배열
## 08-1 제너릭 다루기
> 제너릭은 클래스 내부에서 사용할 자료형을 나중에 인스턴스를 생성할 때 확정   
> 나오게 된 배경은 자료형의 객체들을 다루는 메서드나 클래스에서 컴파일 시간에 자료형을 검사해 적당한 자료형을 선택할 수 있도록 하기 위함   
> 객체의 자료형을 컴파일할 때 체크하기 때문에 1.객체 자료형의 안정성을 높임 2.형 변환의 번거로움이 줄어듦

### 제너릭의 일반적인 사용 방법
* 앵글브래킷(`<>`) 사이에 형식 매개변수(대표적으로 `T`)를 하나 이상 넣어 선언
* 형식 매개변수는 나중에 필요한 자료형으로 대체됨
* 제너릭은 다양한 자료형을 다뤄야 하는 컬렉션에 많이 사용
* 장점
	1. 의도하지 않은 자료형의 객체를 지정하는 것을 막음   
	2. 객체를 사용할 때 원래의 자료형에서 다른 자료형으로 형 변환 시 발생할 수 있는 오류를 줄여 주는 것
#### 제너릭 클래스
> 형식 매개변수를 1개 이상 받는 클래스   
	
* 클래스를 선언할 때 자료형을 특정 X   
* 인스턴스를 생성하는 시점에서 클래스의 자료형을 정하는 것   
* 형식 매개변수를 클래스의 프로퍼티에 사용하는 경우 **클래스 내부에서는 사용할 수 없음**
	> 자료형이 특정되지 못하므로 인스턴스를 생성할 수 없기 때문
* 대신 **주 생성자**나 **부 생성자**에 형식 매개변수를 지정해 사용 가능

#### 자료형 변환
> 일반적으로 상위 클래스와 하위 클래스의 선언 형태에 따라 클래스의 자료형을 변환할 수 있지만   
> 제너릭 클래스는 가변성을 지정하지 않으면 형식 매개변수에 상·하위 클래스가 지정되어도 서로 자료형이 변환되지 않음
#### 형식 매개변수의 null 제어
> 제너릭의 형식 매개변수는 기본적으로 null 가능한 형태로 선언
* 형식 매개변수에 특정 자료형을 지정하면 null 을 **제한**
#### 제네릭 함수 혹은 메서드
> 형식 매개변수를 받는 함수나 메서드를 제너릭 함수 또는 메서드라고 함
* 앞쪽에 `<T>`와 같이 형식 매개변수를 지정(`<K, V>`처럼 여러개도 가능)
* 자료형의 결정은 함수가 **호출될 때** 컴파일러가 자료형을 추론할 수 있음
* 이 자료형은 **반환 자료형**과 **매개변수 자료형**에 사용 가능
#### 제네릭과 람다식
* 형식 매개변수로 선언된 함수의 매개변수를 연산할 경우에는 자료형을 결정할 수 없기 때문에 오류
* 람다식을 매개변수로 받으면 자료형을 결정하지 않아도 실행 시 람다식 본문을 넘겨줄 때 결정되므로 해결

### 자료형 제한하기
> 제네릭 클래스나 메서드가 받는 형식 매개변수를 특정한 자료형으로 제한할 수 있음   
> 자바에서는 `extends`나 `super`를 사용해 자료형을 제한   
> 코틀린에서는 콜론(`:`)을 사용해 제한
#### 클래스에서 형식 매개변수의 자료형 제한하기
#### 함수에서 형식 매개변수의 자료형 제한하기
#### 다수 조건의 형식 매개변수 제한하기
* 형식 매개변수의 사용 범위를 지정하는 `where` 키워드를 사용

### 상·하위 형식의 가변성 (뭔소리지) p.361
> 가변성이란 형식 매개변수가 클래스 계층에 영향을 주는 것   
> ex) 형식 A의 값이 필요한 모든 클래스에 형식 B의 값을 넣어도 아무 문제가 없다면 B는 A의 하위형식(Subtype)
#### 클래스와 자료형
|형태|클래스인가?|자료형인가?|
|:---:|:---:|:---:|
|String|네|네|
|String?|아니오|네|
|List|네|네|
|List\<String\>|아니오|네|

* 하위 클래스는 상위 클래스가 수용할 수 있음
#### 가변성의 3가지 유형
|용어|의미|
|:---:|:---:|
|공변성(Covariance)|T'가 T의 하위 자료형이면, C<T'>는 C<T>의 하위 자료형이다. 생산자 입장의 out 성질|
|반공변성(Contravariance)|T'가 T의 하위 자료형이면, C<T>는 C<T'>의 하위 자료형이다. 생산자 입장의 in 성질|
|무변성(Invariance)|C<T>는 C<T'>는 아무 관계가 없다. 생산자 + 소비자|

#### 무변성
#### 공변성
* 형식 매개변수의 상하 자료형 관계가 성립하고, 그 관계가 그대로 인스턴스 자료형 관계로 이어지는 경우
* `out` 키워드 사용
#### 반공변성
* 자료형의 상하 관계가 **반대**가 되어 인스턴스의 자료형이 상위 자료형이 됩니다.
* `in` 키워드 사용
#### 공변성에 따른 자료형 제한하기

### 자료형 프로젝션
#### 가변성의 2가지 방법
* 선언 지점 변성   
클래스를 **선언하면서** 클래스 자체에 가변성을 지정하는 방식   
클래스를 선언하면서 가변성을 지정하면 클래스의 공변성을 전체적으로 지정하는 것이 되기 때문에   
클래스를 사용하는 장소에서 따로 자료형을 지정해 줄 필요가 없어 편리

* 사용 지점 변성   
메서드 매개변수에서 또는 제너릭 클래스를 생성할 때와 같이 **사용 위치에서** 가변성을 지정하는 방식   

#### 사용 지점 변성과 자료형 프로젝션
	> 사용하고자 하는 요소의 특정 자료형에 `in` 혹은 `out`을 지정해 제한하는것을 자료형 프로젝션
#### 스타 프로젝션
* `Box<*>`   
어떤 자료형이라도 들어올 수 있으나 구체적으로 자료형이 결정되고 난 후에는   
그 자료형과 하위 자료형의 요소만 담을 수 있도록 제한할 수 있음

* `Nothing` 클래스
	> 코틀린의 최하위 자료형으로 아무것도 가지고 있지 않은 클래스   
	> 최상위의 `Any`와는 정반대   
	> `Nothing`은 보통 아무것도 존재하지 않는 값을 표현할 때 사용
#### 자료형 프로젝션의 정리
|종류|예|가변성|제한|
|:---:|:---:|:---:|:---:|
|out 프로젝션|`Box<out Cat>`|공변성|형식 매개변수는 세터를 통해 값을 설정하는 것이 제한된다|
|in 프로젝션|`Box<in Cat>`|반공변성|형식 매개변수는 게터를 통해 값을 읽거나 반환할 수 있다|
|스타 프로젝션|`Box<*>`|모든 인스턴스는 하위 형식이 될 수 있다|in과 out은 사용 방법에 따라 결정된다|

### reified 자료형 ?????????????????????
> reified는 우리말로 '구체화된'이란 뜻
<T> 처럼 결정되지 않은 제너릭 자료형은 컴파일 시간에는 접근 가능하나 함수 내부에서 사용하려면   
함수의 매개변수를 넣어 `c: Class<T>`처럼 지정해야만 실행 시간에 사라지지 안혹 접근 가능 -> 불편   
`reified`로 형식 매개변수 T를 지정하면 실행 시간에 접근 가능
* reified 자료형은 **인라인 함수**에서만 사용 가능
* reified T 자료형은 컴파일러가 복사해 넣을 때 실제 자료형을 알 수 있기 

## 08-2 배열 다루기
> 코틀린에서 배열은 `Array` 클래스로 표현   
> `java.util.Arrays` : 배열을 사용하기위한 자바 표준 라이브러리
### 배열을 사용하는 방법
#### 기본적인 배열 표현
* `arrayOf()` : 괄호안의 요소들로 초기화
	> `arrayOf<자료형>()` : 특정 자료형으로만 제한   
	> ex) `arrayOf<Int>()`   
	> `자료형+Array()` : 특정 자료형으로만 제한   
	> ex) `intArrayOf()`, `byteArrayOf()`, `shortArrayOf()`, `longArrayOf()`, `booleanArrayOf()`, `charArrayOf()`, ...   
	> ex) `ubyteArrayOf()`, `ushortArrayOf()`, `uintArrayOf()`, `ulongArrayOf()` -> 부호 없는 정수의 자료형
* `Array()` : Array 클래스 생성자
* `arrayOfNulss()` : 빈 상태의 배열
#### 다차원 배열
#### 배열에 여러 가지 자료형 혼합하기
> 특정 자료형으로 제한하지 않는다면 배열의 요소로 여러 가지 자료형을 혼합할 수 있음
#### 배열 요소에 접근하기
* Array 클래스는 코틀린의 표준 라이브러리. 다음과 같이 선언되어 있음.
```
public class Array<T>{
	public inline constructor(size: Int, init: (Int) -> T)
	public operator fun get(index: Int): T
	public operator fun set(index: Int, value: T): Unit
	public val size: Int
	public poerator fun iterator(): Iterator<T>
}
```
`get()`, `set()` 메서드를 가지고 있는데 이것은 요소에 접근하기 위한 게터/세터.   
대괄호를 사용해도 접근할 수 있는데 이것은 **연산자 오버로딩**으로 정의되어 있기 때문   
#### 배열의 내용 한꺼번에 출력하기
* `toString()` : 배열의 내용을 한꺼번에 출력(자바의 표준 라이브러리 Arrays에서의 멤버 메서드)
* `deepToString()` : 다차원 배열을 표시하고자 할때
#### 표현식을 통해 배열 생성하기
|val\|var 변수이름 = Array(요소 개수, 초깃값)|
|---|
* 두 번째 인자는 람다식 초깃값 `init: (Int) -> T`(위의 `constructor` 확인)
	> ex) `val arr3 = Array(5, {i -> i * 2})`
* 요소 개수가 많은 배열을 생성하려면 `arrayOfNulls`를 사용하거나 표현식 사용
	> ex) `var a = arrayOfNulls<Int>(1000)`   
	> ex) `var a = Array(1000, {0})`
* 특정 클래스 객체로 배열을 만들려면 다양한 **람다식 표현법**으로 필요한 요소 생성
	> ex) `var a = Array(1000, {i -> myClass(i)})`

* [참고1](https://brunch.co.kr/@mystoryg/27)
* [참고2](https://brunch.co.kr/@mystoryg/47)


### 배열 제한하고 처리하기
> 배열은 일단 정의되면 배열의 길이와 내용이 메모리에 **고정**   
> 고정되지 않은 동적인 배열이 필요하면 컬렉션의 하나인 `List`를 사용해야 함
#### 배열에 요소 추가하고 잘라내기
> 배열이 일단 정의되면 **고정**. 따라서 새로 **할당**하는 방법으로 요소를 추거하거나 잘라냄
* `plus()` : Array 클래스의 멤버메서드? 기존 배열에서 요소를 추가하고 배열을 반환하는 것 같음
```
val arr1 = intArrayOf(1,2,3,4,5)
val arr2 = arr1.plus(6)
```
* `sliceArray()` : Array 클래스의 멤버메서드? 기존 배열에서 요소를 잘라내고 배열을 반환하는 것 같음
`val arr3 = arr1.sliceArray(0..2)` -> 필요한 범위를 잘라내 배열 반환 반환 (요소가 arr1[0],arr1[1],arr1[2] 인 배열이 반환됨)
#### 기타 배열 관련 API 사용하기
* `first()` : 첫 번째 요소 반환
* `last()` : 마지막 요소 반환
* `indexOf()` : 요소 3의 인덱스 출력
* `average()` : 배열의 평균 값 출력
* `count()` : 요소 개수 세기
* `reversedArray()` : 요소의 순서를 완전히 뒤집기
* `reverse()` : 요소의 순서를 완전히 뒤집기 (무슨차이임?)
* `sum()` : 요소를 합산
* `fill()` : 주어진 요소를 채움
* `contains()` : 배열에 특정 요소가 포함되어 있는지 확인(있으면 true 반환)
	> `operator fun <T> Array<out T>.contains(element: T): Boolean`   
	> 이 표현은 결국 중위 표현법으로 `in` 연산자를 사용   
	> `arr.contains(4)` == `4 in arr` 같은 표현임
* 등등..
* [Array 표준 라이브러리](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-array)
#### 다양한 자료형을 위한 Any로 선언된 배열
* 자료형이 지정된 배열은 다른 자료형으로 변환 불가
* 단, `Any` 자료형으로 만들어진 배열은 기존 자료형을 다른 자료형으로 지정할 수 있음
#### 멤버 메서드를 통한 배열 순환하기
* 반복문을 사용한 배열의 순환 말고도 배열의 멤버 메서드를 사용해 요소를 순환
* `forEach()` : 요소 개수만큼 지정한 구문을 반복 실행
* `forEachIndexed()` : 위와 같으며 인덱스까지 추가로 출력
`arr.forEach{element -> print($element)}`
`arr.forEachIndexed({i, e -> println("arr[$i] = $e")})`

* `iterator()` : 반복을 위한 요소를 처리하는 이더레이터
```
val iter: Iterator<Int> = arr.iterator()
while(iter.hasNext()){
	val e = iter.next()
	print("$e ")
}
```

### 배열 정렬하기
> Array는 기본적인 정렬 알고리즘을 제공
#### 기본 배열 정렬하고 반환하기
##### 원본은 그대로 두고 정렬된 배열을 반환
* `sortedArray()`
* `sortedArrayDescending()`
##### 원본 배열에 대한 정렬
* `sort()`
* `sortDescending()`
* 사용할때 그냥 사용해도 되고 `sort(fromIndex, toIndex)` 처럼 범위를 지정해서 정렬할 수도 있음!!
##### 특정 표현식에 따라 정렬
* `sortBy()`
* `sortByDescending()`
* ex) `items.sortBy{item -> item.length}`
##### 컬렉션 목록인 List로 반환
* `sorted()`
* `sortedDescending()`
* `sortedBy()`
* `sortedByDescending()`
#### sortBy()로 데이터 클래스 정렬하기 (데이터클래스 p.317 참고)
* [예제코드](https://github.com/rudeore333/TIL/blob/master/Kotlin/Do%20it!%20%EC%BD%94%ED%8B%80%EB%A6%B0%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/KotlinProgramming/src/chap08/section2/ArraySortedClass.kt)
* Arrays.kt 파일의 함수의 원형
`public inline fun <T, R : Comparable<R>> Array<out T>.sortBy(crossline selector: (T) -> R?): Unit`
**!!Ctrl + B 를 누르고 선언부를 참조해 함수의 정의를 확인해보기!! p.387**
#### sortWith() 비교자로 정렬하기
> 비교자(Comparator)에 의해 정렬하는 방법   
> `sortWith()`는 Array에 확장된 제네릭 메서드
`public fun <T> Array<out T>.sortWith(comparator: Comparator<in T>): Unit`
* [예제코드1](https://github.com/rudeore333/TIL/blob/master/Kotlin/Do%20it!%20%EC%BD%94%ED%8B%80%EB%A6%B0%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/KotlinProgramming/src/chap08/section2/ArraySortedSortWith.kt)
	> Comparator는 자바의 인터페이스로서 2개의 객체를 비교하는 `compare()`를 구현
* [예제코드2](https://github.com/rudeore333/TIL/blob/master/Kotlin/Do%20it!%20%EC%BD%94%ED%8B%80%EB%A6%B0%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/KotlinProgramming/src/chap08/section2/ArraySortedSortWith2.kt)
	> `compareBy()`를 함께 사용하면 이름을 먼저 정렬, 이름이 동일한 경우 가격 기주으로 다시 정렬
#### 배열 필터링하기
* `filter()` 메서드를 활용해 원하는 데이터를 골라내기
```
//0보다 큰 수 골라내기
val arr = arrayOf(1, -2, 3, 4, -5, 0)
arr.filter {e -> e > 0}.forEach{e->print("$e")}
```
```
// a로 시작하는 요소만 골라서 map을 받아 대문자로 변경 후 출력
fun main(){
	val fruits = arrayOf("banana", "avocado", "apple", "kiwi")
	fruits
	.filter {it.startsWith('a')}
	.sortedBy{it}
	.map{it.toUpperCase()}
	.forEach{println(it)}
}
```
* 이렇게 여러 개의 메서드를 연속해서 호출하는 방법을 **메서드 체이닝(Method Chaining)** 이라고 함
* 특정 요소가 있는지 확인하는 방법은 when문과 in을 함께 사용
* `minBy()` : 가장 작은 값
* `maxBy()` : 가장 큰 값
`println(products.minBy{it.price})`
`println(products.maxBy{it.price})`

### 배열 평탄화 하기
> 다차원 배열을 단일 배열로 만드는 것   
* 코틀린 에서는 Array에 `flatten()` 메서드를 통해 평탄화 기능 지원
`val flattenSimpleArray = simpleArray.flatten()`


## 08-3 문자열 다루기
### 문자열의 기본 처리
> 문자열은 연속된 문자의 배열과 같음   
> 문자열은 불변(immutable) 값으로 생성되기 때문에 참조되고 있는 메모리가 변경될 수 없음   
> 새로운 값을 할당하려고 한다면 기존 메모리 이외에 새로운 문자열을 위한 메모리를 만들어 할당
* `var`로 선언하는 경우 전체 문자열을 내부적으로 새로 생성해 **할당**되고 기존 사용하던 메모리 공간은 GC에 의해 제거
* 대량의 문자열을 다룰 때는 메모리의 낭비 등이 일어나지 않도록 주의
#### 문자열 추출하고 병합하기
> 문자열은 특수한 형태의 문자 배열. 따라서 문자열의 각 문자는 특정 인덱스를 가짐.
* 특정 범위의 문자열을 추출하기 위해 `substring()`이나 `subSequence()`를 사용해 특정 인덱스의 범위를 지정할 수 있음

|String.substring(인덱스 범위 지정): String|
|---|

|CharSequence.subSequence(인덱스 범위 지정): CharSequence|
|---|

* 문자열의 특정 인덱스를 바꿀때 앞뒤로 추출하고 바꾼뒤 + 연산자로 병합해 다시 할당
```
var s = "abcdef"
s = s.substring(0..1) + "x" + s.substring(3..s.length-1)
```
#### 문자열 비교하기
* `s1.compareTo(s2) : s1과 s2가 같다면 0, s1이 s2보다 작으면 양수, 그렇지 않으면 음수.
	> 두 번째 인자로 true를 주게되면 대소문자를 무시한다.
#### StringBuilder 사용하기
* 문자열이 사용할 공간을 좀 더 크게 잡을 수 있음 -> 요소를 변경할 때 이 부분을 사용, 특정 단어를 변경 가능
* 기존의 문자열보다 처리 속도가 느림, 변경이 없으면 메모리 낭비
* 문자열이 자주 변경되는 경우에 사용할 것
* **여유분의 공간이 핵심!**

```
var s = StringBuilder("Hello")
s[2] = 'x'
```

* StringBuilder의 기타 관련 메서드를 사용하면 포함(append),추가(insert),삭제(delete)가 용이
* 문자열을 포함시키기 위해 사용하는 `append()`는 **생성된 버퍼**를 사용하므로 보통 +연산자를 이용해 새로운 문자열 객체를 만들어 처리하는 것보다 더 좋음!

```
s.append("World") //뒤에 덧붙임
s.insert(10,"Added") //인덱스 10번부터 추가
s.delete(5,10) // 인덱스 5번부터 10번 "전"까지 삭제
```
#### 기타 문자열 처리
* `toLowerCase()`
* `toUpperCase()`
* `split()` : 매개변수를 기준으로 문자열을 잘라냄. 대체로 컬렉션 List<String>으로 추론되어 할당됨!
	> 분리 문자는 여러개가 될 수도 있다
* `trim()`

#### 문자열을 정수로 변환하기
* `toInt()`
	> 자바의 `Integer.ParseInt`를 사용함
숫자가 아닌 경우 `NumberFormatException` 오류를 발생 -> try~catch 블록으로 처리   
```
try{
"12w".toInt()
} catch(e: NumberFormatException){
  println(e.printStackTrace())
}
```
* `toIntOrNull()` : 숫자가 아닌 문자가 포함되었을 때 null 반환 받고자 할 때

### 리터럴 문자열
> 특수한 문자를 처리하기 위해 백슬래시(\)를 포함한 문자표현인 이스케이프 문자를 사용 가능

|이스케이프 문자의 종류|||
|:---|:---|:---|
|\t 탭(tab)|\r 캐리지 리턴(carriage return|\\ 백슬래시(backslash)|
|\b 백스페이스(backspace)|\\' 작은따옴표(single quote)|\\$ 달러기호(dollar)|
|\n 개행(newline)|\\" 큰따옴표(double quote)||
* 유니코드를 사용할 수 있음 `\uHHHH` 형태로 16진값을 나타냄
* 3중 따옴표(""")를 사용하면 개행문자를 넣지 않고도 원본 문자열 그대로 개행까지 표시 가능
* `trimMargin()`을 사용해 특정 문자 기준으로 공백 제거 가능. 기본값은 파이프 기호(`|`)
#### 형식 문자 사용하기
> 코드의 결괏값을 문자열의 원하는 형태로 나타낼 수 있음
* String에 `format()`을 사용 가능

|inline fun String.format(vararg args:Any?): String (source)|

|형식 문자의 종류|||
|:---|:---|:---|
|%b 참과 거짓의 Boolean 유형|%o 8진 정수|%g 10진 혹은 E 표기법의 실수|
|%d 부호 있는 정수|%t 날짜나 시간|%n 줄 구분|
|%f 10진 실수|%c 문자|%s 문자열|
|%h 해시코드|%e E 표기법의 실수|%x 16진 진수|

```
val pi = 3.1415926
val dec = 10
val s = "hello"
println("pi = %.2f, %3d, %s".format(pi,dec,s))
```

# 09 컬렉션
## 09-1 컬렉션의 구조와 기본
> 자주 사용하는 기초적인 자료구조를 모아놓은 일종의 프레임워크로 표준 라이브러리로 제공   
### 코틀린의 컬렉션
#### 컬렉션의 종류
> List, Set, MAp 등이 있음   
> 자바와 달리 불변형과 가변형으로 나뉨   

**컬렉션의 불변형 자료형 및 가변형 자료형 분류와 그에 따른 생성 헬퍼 함수**
|컬렉션|불변형(읽기 전용)|가변형|
|:---:|:---:|:---:|
|List|listOf|mutableListOf, arrayListOF|
|Set|setOf|mutableSetOf, hashSetOf, linkedSetOf, sortedSetOf|
|Map|mapOf|mutableMapOf, hashMapOf, linkedMapOf, sortedMapOf|

되도록이면 읽기 전용인 불변형으로 선언할 것을 권장

#### 컬렉션 인터페이스
* 가장 상위의 Iterable 인터페이스는 컬렉션이 연속적인 요소를 표현할 수 있도록 함
* `iterator()`는 `hasNext()`와 `next()` 메서드를 가지고 요소를 순환
* Iterable로부터 확장된 Collection 인터페이스는 불변형, 따라서 여기에서 확장된 Set과 List는 읽기 전용 컬렉션

**Collection 인터페이스의 멤버**
|멤버|설명|
|:---:|:---:|
|size|컬렉션의 크기를 나타냄|
|isEmpty()|컬렉션이 비어 있으면 true 반환|
|contains(element: E)|특정 요소가 있으면 true 반환|
|containsAll(elements: Collection<E>)|인자로 받아들인 컬렉션이 있다면 true 반환|
	
* Iterable 인터페이스 아래로 Collection 인터페이스 말고 MutableIterable 과 그 아래의 MutableCollection 인터페이스
* 이 둘은 가변현 컬렉션을 지원하기 위해 준비된 인터페이스

**MutableCollection 인터페이스의 멤버 메서드**
|멤버 메서드|설명|
|:---:|:---:|
|add(element: E)|인자로 전달 받은 요소를 추가하고 true를 반환, 이미 요소가 있거나 중복이 허용되지 않으면 false를 반환|
|remove(element: E)|인자로 저달 받은 요소를 삭제하고 true를 반환, 삭제하려는 요소가 없다면 false를 반환|
|addAll(elements: Collection<E>)|컬렉션을 인자로 전달 받아 모든 요소를 추가하고 true를 반환, 실패하면 false를 반환|
|removeAll(elements: Collection<E>)|컬렉션을 인자로 전달 받아 모든 요소를 삭제하고 true를 반환, 실패하면 false를 반환|
|retainAll(elements: Collection<E>)|인자로 전달 받은 컬렉션의 요소만 보유한다. 성공하면 true를 반환, 실패하면 false를 반환|
|clear()|컬렉션의 모든 요소를 삭제|

## 09-2 List 활용하기
> List는 순서에 따라 정렬된 요소를 가지는 컬렉션   
> 불변형 List를 만들려면 헬퍼 함수인 `listOf()` 사용   
> 가변형 List를 만들려면 `mutableListOf()` 사용   
* 헬퍼 함수 : 보통 List와 같은 컬렉션은 직접 사용해 생성하지 않고 특정 함수의 도움을 통해 생성하는데 이때 사용하는 함수

### 불변형 List 생성하기
#### listOf() 함수
**`listOf()`의 원형**

|public fun <T> listOf(vararg elements: T): List<T>|
|---|

* 형식 매개변수 `<T>`는 원하는 자료형을 지정해 선언할 수 있음
* 사용하지 않으면 `<Any>`가 기본값이며 어떤 자료형이든 혼합할 수 있음

#### 컬렉션 반복하기
* `for(item in fruits){...}` 컬렉션에서 요소를 순환하기 위해 for문을 사용할 수 있음
* `for(index in fruits.indices) {...}` 요소의 인덱스를 통해 List에 접근하려면 컬렉션에 `.indices` 멤버를 추가하면 됨.

#### emptyList() 함수
* 비어 있는 List 생성을 위해 `emptyList<>()` 사용
* **반드시 형식 매개변수를 지정**
`val emptyList: List<String> = emptyList<String>()`

#### listOfNotNull() 함수
* null을 제외한 요소만 반환해 List를 구성
`val nonNullsList: List<Int> = listOfNotNull(2, 45, 2, null, 5 ,null)`

##### List의 주요 멤버 메서드
> List는 앞에서 살펴본 Collection 인터페이스의 메서드를 오버라이딩해 구현

|멤버 메서드|설명|
|:---:|:---:|   
|get(index: Int)|특정 인덱스를 인자로 받아 해당 요소를 반환|
|indexOf(element: E)|인자로 받은 요소가 첫 번째로 나타나는 인덱스를 반환, 없으면 -1 반환|
|lastIndexOf(element: E)|인자로 받은 요소가 마지막으로 나타나는 인덱스를 반환, 없으면 -1 반환|
|listIterator()|목록에 있는 iterator를 반환|
|subList(fromIndex: Int, toIndex: Int)|특정 인덱스의 from과 to 범위에 있는 요소 목록을 반환|

### 가변형 List 생성하기
#### 가변형 arrayListOf() 함수
> `java.util.*` import 필요 (아마 java.util.ArrayList 인거 같음)
* 가변형 헬퍼 함수를 사용하면 요소를 손쉽게 추가하거나 삭제할 수 있는 List 생성
* `arrayListOf()`는 가변형 List를 생성하지만 이것의 **반환 자료형은 자바의 ArrayList**
**`arrayListOf()의 원형`**
|public fun <T> arrayListOf(vararg elements: T): ArrayList<T>|
|---|

#### 가변형 mutableListOf() 함수
* 코틀린의 MutableList 인터페이스를 사용하는 헬퍼 함수 `mutableListOf()`를 통해 가변형 List 생성   
**`mutableListOf()`의 원형**
|public fun <T> mutableListOf(vararg elements: T): MutableList<T>|
|---|

##### 기존의 불변형 List를 가변형을 변경
* `toMutableList()` : 기존의 List는 그대로 두고 새로운 공간을 만들어 냄
* A라는 불변형 List에 `toMutableList()` 하게되면 A' 라는 새로운 불변형 List를 만들어내는 것 같음
   
#### List와 배열의 차이
* Array 클래스에 의해 생성되는 배열 객체는 내부 구조상 **고정된 크기의 메모리**를 가지고 있음
* 코틀린의 List<T>와 MutableList<T>는 인터페이스로 설계되어 있고 이것을 하위에서 특정한 자료구조로 구현
* 따라서 해당 자료구조에 따라 성능이 달라짐
* 예를들어 List<T>인터페이스로부터 구현한 LinkedList<T>와 ArrayList<T>는 특정 자료구조를 가지는 클래스이며 성능도 다름
* List<T>는 Array<T> 처럼 메모리 크기가 고정된 것이 아니기 때문에 자료구조에 따라 늘리거나 줄이는 것이 가능
* Array<T>는 제네릭 관점에서 상·하위 자료형 관계가 성립하지 않는 무변성이기 때문에 Array<Int>는 Array<Number>와 무관
* 코틀린의 MutalbeList<T>도 무관
* List<T>는 공변성이기 때문에 하위인 List<Int>가 List<Number>에 지정될 수 있음

## 09-3 Set과 Map 활용하기
> List : 요소의 중복 가능   
> Set : 집합의 개념 -> 요소의 중복 불가(모든 요소가 유일(Unique))   
> Map : 키와 값의 쌍 형태. 키는 유일, 값은 중복 가능
### Set 생성하기
> 헬퍼 함수인 `setOf()`를 이용해 불변형 Set 생성   
> `mutableSetOf()` 이용해 가변형 Set 생성
#### 불변형 setOf() 함수
* `setOf()` 함수는 읽기 전용인 불변형 Set<T> 자료형을 반환

#### 가변형 mutableSetOf() 함수
* `mutableSetOf()` 함수로 요소의 추가 및 삭제가 가능한 집합 생성
* `mutableSetOf()`는 MutableSet 인터페이스 자료형을 반환하는데, 내부적으로 자바의 LinkedHashSet을 만들어 냄

### Set의 여러 가지 자료구조
#### hashSetOf() 함수
> `java.util.HashSet<T>`

* 헬퍼 함수 `hashSetOf()`를 통해 **해시 테이블**에 요소를 저장할 수 있는 자바의 HashSet 컬렉션을 만듦
* `hashSetOf()`는 자바의 HashSet을 반환
* 불변성 선언이 없음 -> 추가 및 삭제 등의 기능을 수행 가능
* 마찬가지로 입력 순서, 중복된 요소 무시
* 해시값을 통해 요소를 찾아내므로 **검색 속도는 O(1)** 의 상수시간

#### sortedSetOf() 함수
> `java.util.TreeSet<T>`

* `sortedSetOf()` 함수는 자바의 TreeSet 컬렉션을 **정렬된 상태**로 반환
* **레드 블랙 트리 알고리즘** 을 사용 -> 최악의 경우에도 처리에서 일정한 시간을 보장
* HashSet 보다 성능이 좀 떨어지고 시간이 걸리지만 검색과 정렬이 뛰어남
* 불변성 선언이 없음 -> 추가 및 삭제 등의 기능을 수행 가능

#### linkedSetOf() 함수
> `java.util.LinkedHashSet<T>`

* `linkedSetOf()` 함수는 자바의 LinkedHashSet 자료형을 반환하는 헬퍼 함수
* 링크드 리스트 사용해 구현된 해시 테이블에 요소를 저장
* 저장된 순서에 따라 값이 정렬
* HashSet, TreeSet보다 느리지만 포인터 연결을 통해 메모리 저장공간을 좀 더 효율적으로 사용

### Map의 활용
> 내부적으로 자바의 Map을 이용   
> 키와 값으로 구성된 요소를 저장. 여기서 키와 값은 모두 객체.   
> 기존에 저장된 키와 동일한 키로 값을 저장하면 기존의 값은 없어지고 새로운 값으로 대체

#### 불변형 mapOf() 함수
* `mapOf() 함수는 불변형 Map 컬렉션을 만듦

|val map: Map<키 자료형, 값 자료형> = mapOf(키 to 값[, ...])|
|---|
|`val langMap: Map<Int,String> = mapOf(11 to "Java", 22 to "Kotlin", 33 to "C++")`|

**Map에서 사용하는 멤버 프로퍼티와 메서드**
|멤버|설명|
|:---:|:---:|
|size|Map 컬렉션의 크기를 반환|
|keys|Set의 모든 키를 반환|
|values|Set의 모든 값을 반환|
|isEmpty()|Map이 비어 있는지 확인하고 비어 있으면 true를, 아니면 false를 반환|
|containsKey(key: K)|인자에 해당하는 키가 있다면 true를, 없으면 false를 반환|
|containsValue(value: V)|인자에 해당하는 값이 있다면 true를, 없으면 false를 반환|
|get(key: K)|키에 해당하는 값을 반환, 없으면 null을반환|

#### 가변형 mutableMapOf() 함수
* `mutableMapOf()` 함수는 추가, 삭제가 가능한 가변현 Map을 정의
* MutableMap(K,V) 인터페이스 자료형을 반환
* MutableMap은 MutableCollection의 내용을 상속받지 않고 **Map에서 확장**

**MutableMap에서 사용하는 멤버 메서드**
|멤버|설명|
|:---:|:---:|
|put(key: K, value: V)|키와 값의 쌍을 Map에 추가|
|remove(key: K)|키에 해당하는 요소를 Map에서 제거|
|putAll(from: Map<out K,V>)|인자로 주어진 Map 데이터를 갱신하거나 추가|
|clear()|모든 요소를 지움|

#### Map의 기타 자료구조
* 자바의 HashMap, SortedMap, LinkedHashMap 사용 가능
* `hashMapOf()`, `sortedMapOf()`, `linkedMapOf()`로 각각 초기화
* SortedMap은 기본적으로 키에 대해 오름차순 정렬된 형태로 사용
* 내부 구조는 앞서 나온 Set과 비슷하게 해시,트리,링크드리스트의 자료구조로 구현되어 있음

## 09-4 컬렉션의 확장 함수
> 기능을 기준으로 하여 몇가지 범주로 나눌 수 있음

* 연산자(Operator) 기능의 메서드: 더하고 빼는 등의 기능
* 집계(Aggregator) 기능의 메서드: 최대, 최소, 집합, 총합 등의 계산 기능
* 검사(Check) 기능의 메서드: 요소를 검사하고 순환하는 기능
* 필터(Filtering) 기능의 메서드: 원하는 요소를 골라내는 기능
* 변환(Transformer) 기능의 메서드: 뒤집기, 정렬, 자르기 등의 변환 기능

### 컬렉션의 연산
* [예제코드](https://github.com/rudeore333/TIL/tree/master/Kotlin/Do%20it!%20%EC%BD%94%ED%8B%80%EB%A6%B0%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/KotlinProgramming/src/chap09)
* 일반적인 연산자인 `+`와 `-`를 사용해 컬렉션 요소를 하나씩 더하거나 뺄 수 있고
* 컬렉션 자체를 더하거나 뺄 수 있음
* `listOf()`, `Pair()`, `mapOf()` 등을 더하거나 빼는 방법으로 요소를 병합하거나 제거할 수 있음

### 요소의 처리와 집계
* `forEach`, `forEachIndexed`, `onEach`, `count`, `max`, `min`, `maxBy`, `minBy`, `fold`, `reduce`, `sumBy()`
* 뒤에 ()가 명시되지 않은 메소드들은 인자로 함수(람다식)를 받으며 인자를 주지 않으면 ()를 명시해 일반 메소드처럼 사용
#### 요소의 순환
* `forEach` : 각 요소를 람다식으로 처리한 후 **컬렉션을 반환하지 않음**
* `forEachIndexed` : 각 요소를 람다식으로 처리하고 **각 컬렉션을 반환**

```
	list.forEach{print("$it")}
	val returnedList = list.onEach{print(it)}
```
#### 요소의 개수 반환하기
* `count` : 조건에 맞는 요소 개수 반환
```
	println(list.count())
	println(list.count{it % 2 == 0})
```
#### 최댓값과 최솟값의 요소 반환하기
* `max`
* `min`
* `maxBy{}` : 람다식의 결과를 기준으로 최댓값
* `minBy{}` : 람다식의 결과를 기준으로 최솟값
#### 각 요소에 정해진 식 적용하기
* `fold(초깃값){}` : 초깃값과 정해진 식에 따라 처음 요소부터 끝 요소에 적용하며 값을 생성
* `foldRight`
* `reduce{}` : 초깃값 X. fold와 동일
* `reduceRight`
#### 모든 요소 합산하기
* `sumBy` : 람다식에서 도출된 모든 요소를 합한 결과 반환

### 요소의 검사
#### 요소의 일치 여부 검사하기
* `all` : 모든 요소가 일치할 때 true
* `any` : 최소한 하나 이상의 특정 요소가 일치하면 true
#### 특정 요소의 포함 및 존재 여부 검사하기
* `contains()` : 특정 요소가 포함되어 있으면 true
* `containsAll()` : 모든 요소가 포함되어 있으면 true
* `contains()`는 범위 연산자 `in`을 사용해서 요소의 포함 여부를 확인할 수도 있음
```
	println(list.contains(2))
	println(2 in list)
```
* `none` : 람다식에 따라 검사했을 때 요소가 없으면 true
* `isEmpty()` : 컬렉션이 비었으면 true
* `isNotEmpty()` : 안비었으면 true
```
	println(list.none())
	println(list.none{ it > 6 })
```

### 요소의 필터와 추출
#### 특정 요소를 골라내기
* `filter` : 주어진 식의 조건에 따라 골라냄
* `filterNot` : 주어진 식의 조건이 아닌것을 골라냄
* `filterNotNull()` : null을 제외함
* `filterIndexed` : 2개의 인자를 람다식에서 받아서 인덱스와 값에 대해 특정 수식에 맞는 조건을 골라냄
* `filterIndexedTo(반환할 컬렉션){}` : `filterindexed`에 컬렉션으로 반환되는 기능 추가
```
	val mutList = list.filterIndexedTo(mutableListOf()){idx, value -> idx != 1 && value % 2 == 0}
```
* `filterKeys` : 키에 대한 조건에 맞는 부분을 반환
* `filterValues` : 값에 대한 조건에 맞는 부분을 반환
* `filterIsInstance<T>()` : 원하는 자료형의 데이터만 골라냄
#### 특정 범위를 잘라내거나 반환하기
* `slice()` : 특정 범위의 인덱스를 가진 List를 인자로 사용해 기존 List에서 요소들을 잘라냄
```
	println("slice: " + list.slice(listOf(0, 1, 2)))
```
* `take` : n개의 요소를 가진 List를 반환
```
	println(list.take(2))
	println(list.takeLast(2))
	println(list.takeWhile { it < 3 })
```
#### 특정 요소 제외하기
* `drop` : take와는 정반대. n개의 요소를 제외하고 List를 반환
```
	println(list.drop(3))
	println(list.dropWhile { it < 3 })
	println(list.dropLastWhile { it > 3 })
```
#### 각 요소의 반환
* `componentN() : 각 요소는 이것과 대응. 이것을 사용해 요소를 반환. N은 인덱스 번호가 아닌 1부터 시작하는 요소의 순서 번호.
```
	println(list.component1())
```
#### 합집합과 교집합
* `distinct()` : 여러 중복 요소가 있는 경우 1개로 취급해 다시 컬렉션 List로 반환. **합집합과 같은 원리**
* `intersect()` : 겹치는 요소만 골라내 List로 반환. **교집합과 같은 원리**

### 요소의 매핑
* [예제코드](https://github.com/rudeore333/TIL/blob/master/Kotlin/Do%20it!%20%EC%BD%94%ED%8B%80%EB%A6%B0%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/KotlinProgramming/src/chap09/section4/ExtensionMapping.kt)
* `.map()`은 주어진 컬렉션의 요소에 일괄적으로 `.map()`에 있는 식을 적용해 새로운 컬렉션을 만들 수 있게하는 메서드
* `forEach()`와 비슷해 보이나 주어진 컬렉션을 전혀 건드리지 않는다는 점에서 좀 더 안전
* `map`
* `mapIndexed`
* `mapNotNull`
* `flatMap` : 각 요소에 식을 적용한 후 이것을 다시 하나로 합쳐 새로운 컬렉션을 반환
```
	println(list.flatMap{listOf(it, 'A')})
	val result = listOf("abc","12").flatMap(it.toList())
	println(result)
```
* `groupBy` : 주어진 식에 따라 요소를 그룹화하고 이것을 다시 Map으로 반환
```
	val grpMap = list.groupBy { if (it % 2 == 0) "even" else "odd" }
	println(grpMap)
```

### 요소 처리와 검색
* `elementAt()` : 주어진 인덱스에 해당하는 요소를 반환. 인덱스 범위를 벗어나면 IndexOutOfOBoundsException 오류 발생.
* `elementAtOrElse()` : 인덱스 범위를 벗어나도 식에 따라 결과를 반환
* `elementAtOrNull()` : 인덱스 범위를 벗어나는 경우 null 반환
```
	println(list.elementAtOrElse(10, { 2 * it }))
	println(list.elementAtOrElse(10) { 2 * it })
	//인덱스가 10인 요소를 반환하고 범위를 벗어나는 경우 람다식에 따라 결과 반환. (20 반환)
```
* `first`
* `last`
* `firstOrNull`
* `lastOrNull`
* `indexOf()`
* `indexOfFirst`
* `lastIndexOf()`
* `indexOfLast`
* `single` : 해당 조건식에 일치하는 요소를 하나 반환 (요소가 하나 이상인 경우 예외 발생)
* `singleOrNull` : 조건식에 일치하는 요소가 없거나 일치하는 요소가 하나 이상이면 null 반환
* `binarySearch()` : 인자로 주어진 요소에 대해 이진 탐색 후 요소를 반환
> 중복된 요소가 있는 경우 해당 요소가 원하는 순서에 있는 요소인지는 보장하지 않음
* `find` : 조건식을 만족하는 첫 번째 요소를 반환, 없으면 null 반환

### 컬렉션의 분리와 병합
* `union()` : 두 List 컬렉션을 병합하고 중복된 요소 값은 하나만 유지. **Set 컬렉션을  반환**
> `plus`나 `+연산자`를 사용하면 중복 요소를 포함해 합침. List 컬렉션을 반환
* `partition` : 주어진 조건식의 결과(ture와 false)에 따라 List 컬렉션을 2개로 분리. 분리된 2개의 List컬렉션은 **Pair로 반환**
> true는 첫 번째 위치에 반환, false는 두 번째 위치에 반환
* `zip()` : 2개의 컬렉션에서 동일한 인덱스끼리 Pair를 만들어 반환

### 순서와 정렬
* `reversed()` : 순서를 거꾸로 해서 반환
* `sorted()` : 요소를 오름차순 정렬 반환
* `sortedBy` : 특정한 비교식에 의해 오름차순 정렬된 컬렉션 반환
* `sortedDescending()` : 요소를 내림차순 정렬 반환
* `sortedByDescending` : 특정한 비교식에 의해 내림차순 정렬된 컬렉션 반환

## 09-5 시퀀스 활용하기
> 코틀린의 시퀀스는 순차적인 컬렉션으로 요소의 크기를 특정하지 않고, 나중에 결정할 수 있는 특정한 컬렉션.   
> 시퀀스는 처리 중에는 계산하고 있지 않다가 `toList()`나 `count()` 같은 최종 연산에 의해 결정.

### 요소 값 생성하기
#### generateSequence()로 생성하기
* [예제코드](https://github.com/rudeore333/TIL/blob/master/Kotlin/Do%20it!%20%EC%BD%94%ED%8B%80%EB%A6%B0%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/KotlinProgramming/src/chap09/section5/GenerateSequence.kt)
* `generateSequence()` : 시퀀스 생성. 시드(Seed) 인수에 의해 시작 요소의 값이 결정.
```
	val nums: Sequence<Int> = generateSequence(1) { it + 1 }
	println(nums.take(10).toList())
```
* 메서드 체이닝을 쓴다면 하나의 구문이 끝날 때마다 중간 결과로 새로운 List를 계속해서 만들어 냄

### 요소 값 가져오기
#### 메서드 체이닝의 중간 결과 생성하기
* [예제코드](https://github.com/rudeore333/TIL/blob/master/Kotlin/Do%20it!%20%EC%BD%94%ED%8B%80%EB%A6%B0%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/KotlinProgramming/src/chap09/section5/AsSequence.kt)
* `filter`나 `map`을 메서드 체이닝해서 사용할 경우 순차적 연산이기 때문에 시간이 많이 걸릴 수 있음
* `asSequence()` : 중간 연산 결과 없이 한 번에 끝까지 연산한 후 결과를 반환 **병렬 처리**
> **병렬 처리** 하므로 처리 성능이 좋아짐
#### asSequence()를 통해 가져오기
#### asSequence()의 시간 성능
시스템마다 수행 결과는 약간씩 달라질 수 있지만 백만 개의 요소가 있는 목록을 처리하는데 `asSequence()`를 사용하는 경우 비교적 짧은 시간에 수행된 것을 알 수 있음   
다만 작은 컬렉션에는 시퀀스를 사용하지 않는 것이 좋음   
왜냐하면 `filter()` 등은 **인라인 함수**로 설계되어 있는데, 시퀀스를 사용하면 람다식을 저장하는 객체로 표현되기 때문에 인라인 되지 않음 -> 작은 컬렉션에는 오히려 좋지 않음   
또한 한 번 계산된 내용은 메모리에 저장하기 때문에 시퀀스 자체를 인자로 넘기는 형태는 사용하지 않는 것이 좋음.
#### 시퀀스를 응용한 피보나치 수열
#### 시퀀스를 이용한 소수
**GOOD! 개쩐다!**




***
↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓
# [컬렉션 함수]
> _list나 set,map과 같은 컬렉션 또는 배열에 일반 함수 또는 람다 함수 형태를 사용하여_   
> _for문 없이도 아이템을 순회하며 참조하거나 조건을 걸고, 구조의 변경까지 가능한 여러가지 함수_   

`for(item in collection)` for문 말고도 **코틀린의 함수형 언어의 특징을** 활용해 컬렉션 사용   
반복문과 조건문을 사용하는 경우를 대부분 대체할 수 있다는 장점

* forEach : `collection.forEach{}` 중괄호 안에서 collection의 객체들을 `it` 이라는 변수로 순서대로 참조 가능
* filter : `collection.filter{it<4}` 중괄호 안의 조건에 맞는collection의 객체들만 반환
* map : `collection.map{it*2}` 중괄호 안의 수식을 collection의 객체들에 적용해 반환
* any : `collection.any{it == 0}` 하나라도 조건에 맞으면 true
* all : `collection.all{it == 0}` 모두 조건에 맞으면 true
* none : `collection.none{it == 0}` 하나도 조건에 맞지 않으면 true
* first (일반함수) : `collection.first()` 컬렉션의 첫번째 아이템 반환
* first (람다함수) : `collection.first{it>3}` 조건에 맞는 첫번째 아이템을 반환 -> **find로 대체가능**
* last (람다함수) : `collection.last{it>3}` 조건에 맞는 마지막 아이템을 반환 -> **findLast로 대체가능**

first , last 사용할때 조건에 맞는 객체가 없는경우(=컬렉션이 비어있는 경우) 문제발생 -> NoSuchElementException
* firstOrNull : 조건에 맞는 객체가 없는경우 null을 반환
* lastOrNull : 조건에 맞는 객체가 없는경우 null을 반환

* count (일반함수) : `collection.count()` 컬렉션의 모든 아이템의 개수 반환
* count (람다함수) : `collection.count{it>7}` 조건에 맞는 아이템의 개수 반환

* associateBy : `collection.associateBy{it.name}` 객체에서 key를 추출하여 map으로 변환하는 함수   
<img src="/Kotlin/image/associateBy.png" width="40%" height="40%" title="px(픽셀) 크기 설정" alt="associateBy"></img>

* groupBy : `collection.groupBy{it.birthYear}` key가 같은 아이템끼리 배열로 묶어 map으로 만드는 함수   
<img src="/Kotlin/image/groupBy.png" width="40%" height="40%" title="px(픽셀) 크기 설정" alt="groupBy"></img>

* partition : `collection.partition{it.birthYear>2002}` 아이템에 조건을 걸어 **두 개의 컬렉션** 으로 나누어 줌   
<img src="/Kotlin/image/partition.png" width="40%" height="40%" title="px(픽셀) 크기 설정" alt="partition"></img>   
**두 컬렉션은 두 객체를 담을 수 있는 'Pair'라는 클래스 객체로 반환되므로 각각의 컬렉션을 'first' , 'second'로 참조하여 사용**   
**또는 페어를 직접 받아줄 수 있도록 변수이름을 괄호안에 두 개 선언해주면 각각의 변수 이름으로 받을 수 있다**   
`val(over2002, under2002) = collection.partition{it.birthYear>2002}`

* flatMap : `collection.flatMap{listOf(it*3,it+3)}` 아이템마다 만들어진 컬렉션을 합쳐서 반환하는 함수
* getOrElse : `collection.getOrElse(1){50}` 인덱스 위치()에 아이템이 있으면 아이템을 반환하고 아닌 경우 지정한 기본값{}을 반환하는 함수
* zip : `collectionA zip collectionB` 컬렉션 두 개의 아이템을 1:1로 매칭하여 새 컬렉션을 만들어 줌   
**1:1로 매칭하여 pair클래스의 객체로 만든후 list에 넣어 반환**  
**이때 반환된 결과 list의 아이템의 개수는 더 작은 컬렉션을 따라가게 됨**

↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑
***


# 10 표준 함수와 파일 입출력
## 10-1 코틀린 표준 함수
> 코틀린 표준 라이브러리의 다양한 함수들   
> 표준 함수를 이용하면 코드를 더 단순화하고 읽기 좋게 만들어 줌   
> 표준 함수는 람다식과 고차 함수를 이용해 선언되어 있음

### 람다식과 고차 함수 복습하기
> [윗부분정리하고링크걸어두기](https://youtube.com)   
> p.112, p.138 
#### 람다식
#### 고차함수

### 클로저
* 클로저 : 람다식으로 표현된 내부 함수에서 외부 범위에 선언된 변수에 접근할 수 있는 개념
* 포획(capture)한 변수 : 람다식 안에 있는 외부 변수는 값을 유지하기 위해 람다식이 포획한 변수라고 부름
* 클로저 개념에서는 포획한 변수는 **참조가 유지**되어 함수가 종료되어도 사라지지 않고 함수으 ㅣ변수에 접근하거나 수정할 수 있게 해줌
* 클로저의 조건
	1. final 변수를 포획한 경우 변수 값을 람다식과 함께 저장한다.
	2. final이 아닌 변수를 포획한 경우 변수를 특정 래퍼(wrapper)로 감싸서 나중에 변경하거나 읽을 수 있게 한다. 이때 래퍼에 대한 참조를 람다식과 함께 저장한다.


### 코틀린의 표준 라이브러리
#### 확장 함수의 람다식 접근 방법
|함수 이름|람다식의 접근 방법|반환 방법|
|:---:|:---:|:---:|
|T.let|it|block 결과|
|T.also|it|T caller (it)|
|T.apply|this|T caller (this)|
|T.run 또는 run|this|block 결과|
|with|this|Unit|
### let() 함수 활용하기
**let() 표준 함수의 정의**
|`public inline fun <T, R> T.let(block: (T) -> R): R { ... return block(this) }`|
|:---:|
* let() 함수는 제네릭의 확장 함수 형태이므로 어디든 적용 가능
* 매개변수로 람다식 형태인 block이 있고 T를 매개변수로 받아 R을 반환
* let() 함수 역시 R을 반환
* 본문의 this는 객체 T를 가리킴 -> 람다식 결과 부분을 그대로 반환한다는 뜻
#### 커스텀 뷰에서 let() 함수 활용하기
> p.460
#### null 가능성 있는 객체에서 let() 함수 활용하기
> p.461
#### 메서드 체이닝을 사용할 때 let() 함수 활용하기
> p.462

### also() 함수 활용하기
|let() 함수와 also() 함수 차이점 비교|
|:---|
|`public inline fun <T, R> T.let(block: (T) -> R): R = block(this)`|
|`public inline fun <T> T.also(block: (T) -> Unit): T { block(this); return this }`|
* let() 함수는 마지막으로 수행된 코드 블록의 결과를 반환
* also() 함수는 블록 안의 코드 수행 결과와 상관없이 T인 객체 this를 반환
#### 특정 단위의 동작 분리
> p.464

### apply() 함수 활용하기
|이전 함수와 비교|
|:---|
|`public inline fun <T, R> T.let(block: (T) -> R): R = block(this)`|
|`public inline fun <T> T.also(block: (T) -> Unit): T { block(this); return this }`|
|`public inline fun <T> T.apply(block: T.() -> Unit): T { block(); return this }|
* 객체 자체인 this를 반환
* 특정 객체를 생성하면서 함께 호출해야 하는 초기화 코드가 있는 경우 사용
* also()와 다른점은 `T.()` 와 같은 표현에서 람다식이 확장함수로 처리된다는 것
```
	person.also { it.skills = "Java } //it으로 받고 생략 불가
	person.apply { skills = "Swift" } //this로 받고 생략 가능
```
#### 레이아웃을 초기화할 때 apply() 함수 활용하기
> p.467
#### 디렉터리를 생성할 때 apply() 함수 활용하기
> p.467

### run() 함수 활용하기
1. 인자가 없는 익명 함수처럼 동작하는 형태
2. 객체에서 호출하는 형태
* 객체 없이 run() 함수를 사용하면 인자 없는 익명 함수처럼 사용
|run()의 2가지 사용법|
|:---|
|`public inline fun <R> run(block: () -> R): R = return block()`|
|`public inline fun <T ,R> T.run(blcok: T.() -> R): R = return block()`|
* 마지막 표현식을 반환, 마지막 표현식을 구성하지 않으면 Unit 반환

### with() 함수 활용하기
* **receiver**
* 인자로 받는 객체를 이어지는 block의 **receiver**로 전달하며 결괏값을 반환
* run() 함수와 기능이 거의 동일하지만 run()은 receiver가 없다
* with() 함수에서는 receiver로 전달할 객체를 처리하므로 객체의 위치가 달라짐
|public inline fun <T, R> with(receiver: T, block: T.() -> R): R = receiver.block()|
|:---:|
* 매개변수가 2개이므로 `with(){...}`와 같은 형태로 넣어줌
* 확장 함수 형태가 아니고 단독으로 사용되는 함수
* 세이프콜(`?.`)을 지원하지 않기 때문에 let() 함수와 같이 사용되기도 함
* 기본적으로 Unit이 반환되지만, 필요한 경우 마지막 표현식을 반환할 수 있음
* 
### use() 함수 활용하기
* 객체를 사용한 후 `close()` 함수를 자동적으로 호출해 닫아 줌
* 내부 구현을 보면 예외 오류 발생 여부와 상관 없이 항상 `close()`를 호출을 보장
|public inline fun <T : Closeable?, R> T.use(block: (T) -> R): R|
|:---:|

### 기타 함수의 활용
> p.472
#### takeIf() 함수와 takeUnless() 함수의 활용
#### 시간의 측정
#### 난수 생성하기


***
***
# [스코프함수]
> _함수형 언어의 특징을 좀 더 편리하게 사용할 수 있도록 기본 제공하는 함수들_   
> _main함수와 '별도의 scope'에서 인스턴스의 변수와 함수를 조작하므로 코드가 깔끔해지는 장점_

?클래스에서 생성한 인스턴스를 스코프 함수에 전달하면 인스턴스의 속성이나 함수를 스코프 함수 내에서 더 편하게 사용할 수 있도록 하는 기능?

인스턴스의 속성이나 함수를 scope 내에서 깔끔하게 분리하여 사용할 수 있다는 점 때문에 코드의 가독성을 향상시킨다는 장점

* apply
* run
* with
* also
* let

### apply
> 인스턴스를 생성한 후 변수에 담기 전에 '초기화 과정'을 수행할 때 많이 사용
> '인스턴스 자신'을 다시 반환

    fun main() {
        var a = Book("물먹는법특강", 30000).apply{
            name = "[초한정판]" + name
            discount()
        }
    }

    class Book(var name:String, var price:Int){
        fun discount(){
        price -= 2000
        }
    }
    
람다함수 형식으로 참조연산자 없이 바로 사용

인스턴스 자신을 다시 반환하므로 생성되자마자 조작된 인스턴스를 변수에 바로 넣어줄 수 있다.

### run
> 이미 인스턴스가 만들어진 후에 인스턴스의 함수나 속성을 스코프 내에서 사용할 때 유용   
> '마지막 구문'을 반환

    var b = a.run{
        println(a.prince)
        a.name
    }


    fun main() {
        var a = Book("물먹는법특강", 30000).apply{
            name = "[초한정판]" + name
            discount()
        }
        
        a.run{
            println("상품명 : ${name}, 가격 : ${price} 원")
        }
    }

    class Book(var name:String, var price:Int){
        fun discount(){
        price -= 2000
        }
    }
    
### with
> run과 동일한 기능, 단지 인스턴스를 참조연산자 대신 '패러미터'로 받는다는 차이

`a.run{...}` -> `with(a){...}`


### also 와 let
apply/also 는 처리가 끝나면 '인스턴스'를 반환

run/let 은 처리가 끝나면 최종값을 반환

apply, run 과의 차이점으로는 **also** , **let** 은 마치 패러미터로 인스턴스를 넘긴것처럼 `it`을 통해서 인스턴스를 사용할 수 있다.

**이유** : 같은 이름의 변수나 함수가 **'scope 바깥에 중복'**  되어 있는 경우에 혼란을 방지하기 위함

    fun main() {
        var price = 5000
    
        var a = Book("물먹는법특강", 30000).apply{
            name = "[초한정판]" + name
            discount()
        }
        
        a.run{
            println("상품명 : ${name}, 가격 : ${price} 원")
        }
    }

    class Book(var name:String, var price:Int){
        fun discount(){
        price -= 2000
        }
    }

-> `상품명 : [초한정판]물먹는법특강, 5000 원` **price라는 변수가 중복!**


    fun main() {
        var price = 5000
    
        var a = Book("물먹는법특강", 30000).apply{
            name = "[초한정판]" + name
            discount()
        }
        
        a.let{
            println("상품명 : ${it.name}, 가격 : ${it.price} 원")
        }
    }

    class Book(var name:String, var price:Int){
        fun discount(){
        price -= 2000
        }
    }
    
-> `상품명 : [초한정판]물먹는법특강, 28000 원`


***
***
***

## 10-2 람다식과 DSL
> DSL(Domain-Specific Language)이라는 개념으로 특정 주제에 특화된 언어를 만들어 낼 수 있음   
> SQL이 대표적인 DSL   
> P.475
### 코틀린에서 DSL 사용하기
#### DSL 경험해 보기
#### DSL을 구현하는 요소

### DSL을 사용한 사례
#### Spring 프레임워크
#### Spark 프레임워크
#### Ktor 프레임워크

## 10-3 파일 입출력
> P.482
### 표준 입출력의 기본 개념
#### readline() 함수 사용해 보기
#### Kotlin의 입출력 API
#### 자바의 io, nio의 개념
#### 스트림과 채널
#### 넌버퍼와 버퍼 방식
#### 블로킹과 넌블로킹

### 파일에 쓰기
#### File의 PrintWriter 사용하기
#### File의 BufferedWriter 이용하기
#### File의 writeTest() 사용하기
#### FileWriter 사용하기

### 파일에서 읽기
#### File의 FileReader 사용하기
#### 자바의 파일 읽기를 코틀린으로 변경하기
#### copyTo() 사용하기

# 11 코루틴과 동시성 프로그래밍
## 11-1 동시성 프로그래밍
### 블로킹과 넌블로킹
#### 블로킹 동작
#### 넌블로킹 동작

### 프로세스와 스레드
#### 프로세스와 스레드의 개념
#### 스레드 생성하기
#### 사용자 함수를 통한 스레드 생성하기
#### 스레드 풀 사용하기

## 11-2 코루틴의 개념과 사용방법
### 코루틴의 기본 개념
* 코루틴은 비용이 많이 드는 문맥 교환 없이 해당 루틴을 일시중단(suspended)
* 운영체제가 스케줄링에 개입하는 과정이 필요하지 않다
* 일시 중단은 사용자가 제어 가능
#### 코루틴 라이브러리 추가하기
#### 코루틴의 주요 패키지

### launch와 async
* 코루틴에서 사용되는 함수는 suspend()로 선언된 지연 함수여야 코루틴 기능을 사용 가능
* 컴파일러는 suspend가 붙은 함수를 자동적으로 추출해 Continuation 클래스로부터 분리된 루틴을 만듬
* 이러한 **지연 함수**는 코루틴 빌더인 `launch`와 `async`에서 사용할 수 있지만 메인 스레드에서는 사용 불가
* 지연 함수는 또 다른 지연 함수 내에서 사용하거나 코루틴 블록에서만 사용해야 함
#### launch 코루틴 빌더 생성하기
* `launch`를 통해 코루틴 블록을 만들어 내는 것을 코루틴 빌더의 생성이라고 함
* `launch`는 현재 스레드를 차단하지 않고 새로운 코루틴을 실행할 수 있게 하며 특정 결괏값 없이 `Job` 객체를 반환
* `GlobalScope` 실행 범위가 지정되어 있으면 코루틴의 생명 주기가 프로그램의 생명 주기에 의존되므로 `main()`이 종료되면 같이 종료
#### async 코루틴 빌더 생성하기
* `async`도 새로운 코루틴을 실행할 수 있음
* `launch`와 다른 점은 Deferred<T>를 통해 결괏값을 반환한다는 점
* 이때 지연된 결괏값을 받기 위해 `await()`를 사용할 수 있음
#### 코루틴의 문맥
> p.515
#### 시작 시점에 대한 속성
* `CoroutineStart`
	1. DEFAULT : 즉시 시작
	2. LAZY : 코루틴을 느리게 시작(처음에는 중단된 상태이며 start()나 await() 등으로 시작됨)
	3. ATOMIC : 최적화된 방법으로 시작
	4. UNDISPATCHED : 분산 처리 방법으로 시작
	
#### runBlocking의 사용
* `runBlocking`은 새로운 코루틴을 실행하고 완료되기 전까지 현재 스레드를 블로킹
#### join() 함수의 결과 기다리기
* 명시적으로 코루틴의 작업이 완료되는 것을 기다리게 하려면 `Job` 객체의 `join()` 함수를 사용
#### async() 함수의 시작 시점 조절하기
#### 많은 작업의 처리
* 많은 양의 작업을 생성한 코드를 스레드로 바꾸면 Out-of-memory 오류가 발생
* 코루틴으로 작업하면 내부적으로 단 몇 개의 스레드로 수많은 코루틴을 생성해 실행할 수 있기 때문에 오류 발생 
* 메모리나 실행 속도 면에서 큰 장점
* 또 다른 방법으로 `repeat()` 함수를 사용하면 손쉽게 많은 양의 코루틴을 생성할 수 있음

### 코루틴과 시퀀스
* `sequence()`
* 늦은 시퀀스 -> 무제한 스크롤링
* `yield()` 및 `yield()` 함수의 작동 방식
* `take()`
* `yieldAll()`


***
***
***
# [코루틴을 통한 비동기 처리]
> _'비동기'로 여러개의 루틴을 동시에 처리할 수 있는 법_   
> _import kotlinx.coroutines.*_

지금까지 모든 구문을 순차적 '동기적'으로 실행했음   
'여러개의 루틴'을 동시에 실행하여 결과를 내고 싶을때? -> 비동기처리를 지원하는 **코루틴**

코루틴은 메인이 되는 루틴과 별도로 진행이 가능한 루틴으로 개발자가 루틴의 실행, 종료를 마음대로 제어할 수 있는 단위

코루틴을 사용할 때는 kotlinx(코틀린익스텐션)의 coroutines 패키지를 전부 임포트해야함 `import kotlinx.coroutines.*`

코루틴은 **제어범위** 및 **실행범위** 를 지정할 수 있음 -> 이를 **코루틴의 Scope** 라고 함

* GlobalScope : 프로그램 어디서나 제어, 동작이 가능한 기본 범위
* CoroutineScope : 특정한 목적의 Dispatcher를 지정하여 제어 및 동작이 가능한 범위 (새로운 coroutine의 범위)

_Dispatcher란? : 아니 그래서 디스패쳐가 뭐냐니깐?   
`Dispatchers.Default` 백그라운드에서 동작하는 디스패쳐   
`Dispatchers.IO` 네트워크나 디스크등 I/O에 최적화된 동작하는 디스패쳐   
`Dispatchers.Main` 메인(UI) 스레드에서 함께 동작하는 디스패쳐_   
이런 Dispatcher들은 모든 플랫폼에서 지원되지는 않으니 조심해서 사용

코루틴은 이러한 Scope에서 제어되도록 생성될 수 있음
    val scope = CoroutineScope(Dispatcher.Default)
    val coroutineA = scope.launch{}
    val coroutineB = scope.async{}
    
* `launch` : 반환값이 없는 Job 객체
* `async` : 반환값이 있는 Deffered 객체 / 마지막 구문의 결과가 반환   
-> 둘 다 람다함수의 형태

코루틴은 제어되는 스코프 또는 프로그램 전체가 종료되면 함께 종료되기 때문에 코루틴이 끝까지 실행되는 것을 보장하려면   
일정한 범위에서 코루틴이 모두 실행될 때까지 잠시 기다려주어야 한다?

* `runBlocking{}` : 코루틴이 종료될 때까지 메인 루틴을 잠시 대기시켜줌
    runBlocking{
        launch{}
        async{}
    }
**주의 : 안드로이드에서는 메인스레드에서 runBlocking을 걸어주면 일정시간이상 응답이 없는 경우**   
**ANR(Application Not Responding)이 발생하며 앱이 강제 종료됨**

### 예제
    import kotlinx.coroutines.*
    
    fun main(){
        val scope = GlobalScope
        
        scope.launch{
            for(i in 1..5){
                println(i)
            }
        }
        
        runBlocking{
            launch{
                for(i in 1..5){
                    println(i)
                }
            }
        }

    }

## 루틴의 대기를 위한 추가적인 함수들
* `delay(milisecond: Long)` : milisecond 단위로 루틴을 잠시 대기시키는 함수
* `join()` `Job.join()` : Job객체에서 호출하여 Job의 실행이 끝날때까지 대기하는 함수
* `await()` `Deferred.await()` : Deferred 객체에서 호출하여 Deferred의 실행이 끝날때까지 대기하는 함수 / **Deferred의 결과도 반환함**

세 함수들은 코루틴 내부 또는 runBlocking{}과 같은 루틴의 대기가 가능한 구문 안에서만 동작이 가능

### 예제
    import kotlinx.coroutines.*
    
    fun main(){
        runBlocking{
            val a = launch{
                for(i in 1..5){
                    println(i)
                    delay(10)
                }
            }
            val b = async{
                "async 종료"
            }
            
            println("async 대기")
            println(b.await())
            
            println("launch 대기")
            a.join()
            println("launch 종료")
            
        }

    }

## 코루틴 실행 도중 중단하는 방법
* `cancel()` : 코루틴에 cancel()을 걸어주면 두 가지 조건이 발생하며 코루틴을 중단시킬 수 있음
1. 코루틴 내부의 delay() 함수 또는 yield() 함수가 사용된 위치까지 수행된 뒤 종료
2. cancel()로 인해 코루틴 내부의 속성인 isActive가 false가 되므로 이를 확인하여 코드를 통해 **수동** 으로 종료

### 예제
    import kotlinx.coroutines.*
    
    fun main(){
        runBlocking{
            val a = launch{
                for(i in 1..5){
                    println(i)
                    delay(10)
                }
            }
            val b = async{
                "async 종료"
            }
            
            println("async 대기")
            println(b.await())
            
            println("launch 대기")
            a.cancel()
            println("launch 종료")
            
        }

    }

## withTimeoutOrNull()
> _제한시간 내에 수행되면 결과값을 아닌 경우 null을 반환_   
> _withTimeoutOrNull(밀리세컨드단위의시간)_   
> **join() 이나 await() 처럼 blocking 함수임!**

    witTimeoutOrNull(50){
        for(i in 1..1000){
            println(i)
            delay(10)
        }
        "Finish"
    }
    
### 예제
    import kotlinx.coroutines.*
    
    fun main(){
        run Blocking{
            var result = withTimeoutOrNull(50){
                for(i in 1..10){
                    println(i)
                    delay(10)
                }
                "Finish"
            }
            println(result)
        }
    }
-> 1 2 3 null

***
***
***
↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓
## 변수의 동일성 체크 (더 추가할 것)

* **내용의 동일성** : 메모리상에 서로 다른곳에 할당된 객체라도 **그 내용이 같다면 동일** 하다고 판단하는 것
* **객체의 동일성** : 서로 다른 변수가 **메모리상에 같은 객체를 가르킬때만 동일** 하다고 판단하는 것

내용의 동일성을 판단하는 연산자 `==`   
객체의 동일성을 판단하는 연산자 `===`

!'내용의 동일성'은 자동으로 판단되는 것이 아닌 코틀린의 모든 클래스가 내부적으로 상속받는 'Any' 라는 최상위 클래스의 `equals()` 함수가 반환하는 Boolean 값으로 판단!

기본 자료형에는 자료형의 특징에 따라 equals() 함수가 이미 구현되어 있지만 커스텀 class를 만들때는 `open fun equals(other: Any?):Boolean` equals 함수를 상속받아   
동일성을 확인해주는 구문을 **별도로 구현해야 함**
↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑
***
***
***




































***
***
***
***
***
***
***
***
***
***
***
***
***
***
***
***
***


# **[변수와 자료형, 연산자]**
> _클래스 이름은 파스칼 표기법 (ClassName)_   
> _함수나 변수 이름은 카멜 표기법 (functionName)_   
> _!자바와 달리 코틀린의 모든 자료형은 객체! -> 참조형 자료형_

* **var** : 일반적으로 통용되는 변수, 언제든지 읽기쓰기 가능
* **val** : 선언시 초기화, 중간에 값 변경 불가 -> _val로 선언해서 사용하고 나중에 변경이 필요하면 그때가서 var로 바꾸는게 좋다?_

**여기서 val은 최초에 변수에 할당했던 객체 대신 다른 객체를 할당할 수 없다는 얘기임. val A에 MutableList를 할당하고 그 객체의 내부 구조에 따라 데이터를 조작할 수 있지만**   
**앞서 할당한 val A에 다른 MutableList를 할당할 수는 없다는 뜻.**

**Property(속성)** : 클래스에 선언된 변수

**Local Variable(로컬변수)** : 이 외의 Scope 내에 선언된 변수

~`var a : Int` -> 코틀린은 기본변수에서 null을 허용하지 않고 초기화하지않으면 컴파일이 안된다. 의도치않는 에러나 null pointer exception을 원천적으로 차단?~
`val a : Int` -> 자료형만 지정해주면 변수를 선언'만' 할 수 있음

`var a : Int? = null` -> 자료형 뒤에 물음표를 붙여 nullable 변수로 활용 가능. 꼭 필요할때만 사용할것

lateinit , lazy 속성은 추후 추가예정

### 정수자료형
> 명시하지 않으면 웬만하면 Int로 추론

**부호가 있는 정수 자료형**
* Byte 1Bytes	_[-2^7 ~ 2^7 - 1 (-128 ~ 127)]_
* Short 2Bytes	_[-2^15 ~ 2^15 - 1 (-32,768 ~ 32,767)]_
* Int 4Bytes	_[-2^31 ~ 2^31 - 1]_
* Long 8Bytes	_[-2^63 ~ 2^63 - 1]_

**부호가 없는 정수 자료형**
* UByte 1bytes	_[0 ~ 2^8 - 1 (0 ~ 255)]_
* UShort 2Bytes	_[0 ~ 2^16 - 1 (0 ~ 65,535)]_
* UInt 4Bytes	_[0 ~ 2^32 - 1]_
* ULong 8Bytes	_[0 ~ 2^64 - 1]_

코틀린에서 자리수가 많아지면 언더스코어 `_` 로 자리수를 구분한다.   
`val num = 1_000_000`


### 실수자료형
> 명시하지 않으면 Double로 추론

* Float 4bytes
* Double 8bytes -> 기본

부동 소수점 : `3.14e2` , `3.14e-2`

부동 소수점으로 표현할 때 가수 부분이 **52비트**를 넘어가면 **오차** 주의!

### 정수,실수 자료형의 최솟값과 최댓값
> _`MIN_VALUE` 와 `MAX_VALUE` 사용_

`Byte.MIN_VALUE` , `Byte.MAX_VALUE` ...


### 문자자료형

* Char 2bytes	[0 ~ 2^15 -1 (\u0000 ~ \uffff)]

문자 자료형의 선언과 사용을 구분하여 기억!   
문자 자료형 값을 저장할 때 문자 세트(아스키코드 표, 유니코드 표)를 참고하여 **'번호'**로 저장.   
!선언할 때 만큼은 **문자 값으로 선언**!   
선언한 다음에는 문자 자료형에 숫자를 더하는 방식 가능

`toChar()` : 정숫값을 문자로 변환
ex) `65.toChar()` == 'A'

### 논리형

* Boolean

### 정수형 리터럴
> _2진수 10진수 16진수. (8진수는 지원 X)_

`var intValue:Int = 1234`
 
`var longValue:Long = 1234L` <- 접미사 L

`var intValueByHex:Int = 0x1af` _16진수_ <- 접두사 0x

`var intValueByBin:Int = 0b10110110` _2진수_ <- 접두사 0b

### 실수형 리터럴

`var doubleValue:Double = 123.5`

`var doubleValueWithExp:Double = 123.5e10` -> 지수표기법

### Char의 리터럴
> _코틀린은 내부적으로 문자열을 유니코드 인코딩 중에 한 방식인 UTF-16 BE로 관리_   
> _따라서 글자 하나하나가 2bytes의 메모리 공간을 사용_

`var charValue:Char = 'a'`

`var koreanCharValue:Char = '가'`

`\t` : 탭
`\b` : 백스페이스
`\r` : 첫 열로 커서 옮김
`\n` : 개행
`\'` : 작은 따옴표
`\"` : 큰 따옴표
`\\` : 역 슬래시
`\$` : $ 문자
`\uxxxx` : 유니코드 문자

### Boolean의 리터럴

`var booleanValue:Boolean = true`

### 문자열

`val stringValue = "문자열"`

`val multiLineStringValue = """여러 줄의 문자열"""` -> 줄바꿈이나 특수문자까지 그대로 문자열로 사용

### 따옴표 안에서 변수출력

> _변수 앞에 $ 를 붙여 출력_

`println("i : $i, j : $j")`   
`println("안녕하세요. ${personA.birthYear}년생 ${personA.name} 입니다.")` -> println이 문자로 오인할 수 있기때문에 {}로 감싼것   
역슬래쉬 `\` 대신 `${''}` 도 사용가능.

***


# [형변환과 배열]

## 형변환
> _형변환 함수를 제공_ -> **명시적 형변환**   
> _코틀린에는 '암시적 형병환' 지원하지 않음_

`toByte()` `toShort()` `toInt()` `toLong()` `toFloat()` `toDouble()` `toChar()`

`var a: Int = 54321`

`var b: Long = a` -> Type dismatch

`var c: Long = a.toLong()`

## 배열
> _Array\<T\>_     _T는 제너릭_

`var intArr = arrayOf(1, 2, 3, 4, 5)`

`var nullArr = arrayOfNulls<Int>(5)` -> 비어있는 배열

`intArr[2]` 의 값은 `3`

### 더 다양한 Array 메소드들 / 디모 설명 너무 빈약
* https://brunch.co.kr/@mystoryg/27
* https://brunch.co.kr/@mystoryg/47


***


# [타입추론과 함수]

## 타입추론
> **타입추론** : _변수나 함수들을 선언할 때나 연산이 이루어 질 때 자료형을 코드에 명시하지 않아도 코틀린이 자동으로 자료형을 추론해주는 기능_   
> _명시가 필요한 상황이 아니면 타입추론을 이용해 코드량을 줄임_

`val stringValue`**:String**` = "문자열"`

`var intArr`**:Array\<Int\>**` = arrayOf(1,2,3,4,5)`

`var a = 1234` -> Int

`var b= 1234L` -> Long

`var c = 12.45` -> Double

`var d = 12.45f` -> Float

`var e = 0xABCD` -> Int

`var f = 0b0101010` -> Int

`var g = true` -> Boolean

`var h = 'c'` -> Char

## 함수

`fun add(a: Int, b: Int, c: Int): Int` -> 함수 뒤에 있는 `: Int`는 반환형. 반환값이 없다면 생략가능.

`fun add(a: Int, b: Int, c: Int): Int { return a+b+c }`

`fun babo(a: Any) { }` -> **Any** 라는 자료형은 어떤 자료형이든 상관없이 호환되는 코틀린의 **최상위 자료형**

### 단일 표현식 함수
> _반환형의 타입추론이 가능_ -> 반환형 생략가능

`fun add(a: Int, b: Int, c: Int) = a + b + c`


***


# [조건문과 비교연산자]

## if
`if (a>10){ }`
`else { }`

### if의 반환 표현식
코드 블럭의 맨 마지막 줄이 반환값이 된다.

	val isOdd = if(num % 2 == 1) {
			println("홀수입니다.")
        		true
    	    } else {
    		println("짝수입니다.")
        		false
    	    }

### is연산자 / !is연산자

`a is Int` -> 좌측 변수가 우측 자료형인지 **'호환'** 되는지 여부를 체크하고 **'형변환'** 까지 한번에 진행

## when
> _다른 언어에서의 switch case_

    when(a) {
    1 -> println("정수 1입니다")
    "Babo" -> println("바보입니다")
    is Long -> println("Long 타입 입니다")
    !is String -> println("String 타입이 아닙니다")
    else -> println("어떤 조건도 만족하지 않습니다")
    }

### when의 동작 대신 반환하게하는 표현식으로써의 역할

    var result = when(a) {
    1 -> "정수 1입니다"
    "Babo" -> "바보입니다"
    is Long -> "Long 타입 입니다"
    !is String -> "String 타입이 아닙니다"
    else -> "어떤 조건도 만족하지 않습니다"
    }


***


# [반복문과 증감연산자]
## 반복문
> _조건형 반복문_ while do...while   
> _범위형 반복문_

### 조건형 반복문

`while(a<5){ println(a++) }`

`do{ println(a++) } while(a<5)` -> 최초 한번은 구문을 실행함.

### 범위형 반복문
> _사람이 좀 더 이해하기 쉬운 방법_   
> _인덱스로 사용할 변수에는 var등을 붙이지 않아도 됨_

`for(i in 0..9) { print(i) }` -> 0123456789

`for(i in 0..9 step 3){ print(i) }` -> 0369

`for(i in 9 downTo 0){ print(i) }` -> 9876543210

`for(i in 9 downTo 0 step 3){ print(i) }` -> 9630

`for(i in 'a'..'e') { print(i) }` -> abcde

## 증감연산자
`++a a++` 증가연산자 (전위연산자 후위연산자)

`--a a--` 감소연산자 (전위연산자 후위연산자)

전위연산자 : '해당 구문'부터 연산적용 후 사용

후위연산자 : '다음 구문'부터 연산적용 후 사용


***


# [흐름제어와 논리연산자]
## 흐름제어
> _코틀린은 다중 반복문에서 break나 continue가 적용되는 반복문을 lable을 통해 지정할 수 있다._

* `return` : 함수를 '종료'하고 값을 '**반환**'
* `break` : 반복문 내의 구문이 실행되는 중간에 즉시 반복문을 '종료'하고 다음 구문으로 넘어감
* `continue` : 다음 반복조건으로 즉시 넘어감


### 레이블
> _레이블이 달린 반복문을 기준으로 즉시 흐름제어_

**레이블 이름@** ---> **break@loop**

    loop@for (i in 1..0) {
        for(j in 1..10){
            if(1 == 1 && j == 2) break@loop
        }
    }

## 논리연산자
> _논리 값을 연산하여 새로운 논리값을 도출할 때 쓰는 연산자_

* `&&` : and 연산자
* `||` : or 연산자
* `!` : not 연산자

## 비트연산자

* `and` : and 연산자 (자바에서 & 연산자)
* `or` : or 연산자 (자바에서 | 연산자)
* `xor` : xor 연산자 (자바에서 ^ 연산자)
* `inv` : not 연산자 (자바에서 ~ 연산자)
* `sh1` : 왼쪽 쉬프트 연산자 (자바에서 << 연산자)
* `shr` : 오른쪽 쉬프트 연산자 (자바에서 >> 연산자)
* `ushr` : 부호비트 포함 오른쪽 쉬프트 연산자 (자바에서 >>> 연산자)


    ddshl - signed shift left (equivalent of << operator)   
    shr - signed shift right (equivalent of >> operator)   
    ushr- unsigned shift right (equivalent of >>> operator)   
    and - bitwise and (equivalent of & operator)   
    or - bitwise or (equivalent of | operator)   
    xor - bitwise xor (equivalent of ^ operator)   
    inv - bitwise complement (equivalent of ~ operator)   

    1 shl 2 // Equivalent to 1.shl(2), 출력 = 4   
    16 shr 2 // 출력 = 4   
    2 and 4 // 출력 = 0   
    2 or 3 // 출력 = 3   
    4 xor 5 // 출력 = 1   
    4.inv() // 출력 = -5   


***


# [클래스]
## 클래스의 기본 구조
> _객체들의 집합_   
> _클래스는 '값'과 그 값을 사용하는 '기능들을 묶어놓은것_   
> _기본 자료형들도 코틀린 내부에서는 전부 클래스_


**클래스** = **속성** + **함수** (고유의 특징값 + 기능의 구현)


`class Person (var name:String, val birthYear:Int)` -> 함수 없는 클래스의 선언

    class Person (var name:String, val birthYear:Int) {
        fun introduce(){
            println("안녕하세요. ${birthYear}년생 ${name} 입니다.")
        }
    }


### 인스턴스
> _클래스를 이용해서 만들어 내는 서로 다른 속성의 객체를 지칭하는 용어_

`var personA = Person("강석원", 1995)` -> 인스턴스 생성

`Person("강석원", 1995).introduce()` -> 이것과 같이 인스턴스를 변수에 담지 않고도 바로 사용할 수도 있다. 익명객체형식임!


### 참조연산자
> _변수명.속성명 -> '.' 이 참조연산자_

`println("안녕하세요. ${personA.birthYear}년생 ${personA.name} 입니다.")` -> println이 문자로 오인할 수 있기때문에 {}로 감싼것

`personA.introduce()`


## 클래스의 생성자
> _생성자 : 새로운 인스턴스를 만들기 위해 호출하는 특수한 함수_   
> _생성자를 호출하면 클래스의 인스턴스를 만들어 '반환'받음_   
> _1. 인스턴스의 속성을 초기화_   
> _2. 인스턴스 생성시 구문을 수행_

* **기본 생성자** : 클래스를 만들 때 기본으로 선언

* **보조 생성자** : 필요에 따라 추가적으로 선언


`class Person` **(var name:String, val birthYear:Int)** -> 클래스의 '속성'들을 선언함과 동시에 '생성자' 역시 선언하는 방법


### init
> _인스턴스 생성시 구문 수행_   
> _패러미터나 반황형이 없는 특수한 함수_   
> _생성자를 통해 인스턴스가 만들어질 때 호출되는 함수_

    class Person (var name:String, val birthYear:Int) {
        init {
            pirntln ("${this.birthYear}년생 ${this.name}님 생성")
        }
    }

`this` : 인스턴스 자신의 속성이나 함수를 호출하기 위해 **클래스 내부에서 사용** 되는 키워드


### 보조생성자
> _기본 생성자와 다른 형태의 생성자를 제공하여 인스턴스 생성시 편의를 제공하거나 추가적인 구문을 수행하는 기능을 제공하는 역할_   
> **constructor()**

**!보조생성자를 만들때는 반드시 기본생성자를 통해 속성을 초기화 해줘야 함!**

    class Person (var name:String, val birthYear:Int) {
        init {
            pirntln ("${this.birthYear}년생 ${this.name}님 생성")
        }
        
        constructor(name:String) : this(name,1995) {
            println ("보조 생성자가 사용됨")
        }
    }

## 클래스의 상속
> _코틀린은 상속 금지가 기본값_   
> _1. 서브 클래스는 슈퍼 클래스에 존재하는 속성과 '같은 이름'의 속성을 가질 수 없음_   
> _2. 서브 클래스가 생성될 때 반드시 슈퍼 클래스의 생성자까지 호출되어야 함_

### open
> _클래스가 상속될 수 있도록 클래스 선언시 붙여줄 수 있는 키워드_

    open class Animal (var name:String, var age:Int, type:String) {
        fun introduce() {
        println("저는 ${type} ${name}이고, ${age}살 입니다.")
        }
    }
    
    class Dog (name:String, age:Int) : Animal (name, age, "개"){
        fun bark() {
            println("멍멍")
        }
    }
    
**!지나친 상속구조는 코드를 더 어렵게 만든다!**


***


# [오버라이딩과 추상화]
## 오버라이딩
> _서브클래스에서 수퍼클래스와 같은이름과 형태를 가진 함수를 만들 수 없다_   
> _수퍼클래스에서 허용해주면 오버라이딩이 가능하다._

### open
> _상속과 마찬가지로 수퍼클래스에서는 함수 앞에 open 키워드를 붙여주는 것으로 오버라이딩 허용_

    open class Animal {
        open fun eat() {
        println("음식을 먹습니다")
        }
    }
    
### override
> _서브클래스에서는 함수 앞에 override 키워드를 붙여주는 것으로 오버라이딩_

    class Tiger : Animal(){
        override fun eat() {
            println("고기를 뜯습니다")
        }
    }

## 추상화
> _추상함수 : 선언부만 있고 기능이 구현되지 않은 함수_   
> _추상클래스 : 추상함수를 포함하는 클래스_

### abstact
> _클래스 앞에 abstract 키워드를 붙여주는 것으로 추상화_

    abstract class Animal {
        abstract fun eat()
        fun sniff() {
            println("킁킁")
        }
    }
    
    class Rabbit : Animal() {
        override fun eat(){
            println("당근을 먹습니다.")
        }
    }
    
### 인터페이스
> _추상함수로만 이루어져있는 '순수 추상화 기능' 이라고 알려져있지만_   
> _코틀린에서는 인터페이스가 속성,추상함수,일반함수 모두 가질 수 있다._   
> _다만 추상함수는 생성자를 가질 수 있는 반면 인터페이스는 불가능!!!!!_   
> _여러개의 인터페이스 상속 가능_

* 구현부가 있는 함수 -> open 함수로 간주
* 구현부가 없는 함수 -> abstract 함수로 간주

**!따라서, 별도의 open , abstract 키워드가 없어도 포함된 모든 함수를 서브클래스에서 구현 및 재정의가 가능!**

    interface Runner{
        fun run()
    }
    
    interface Eater{
        fun eat(){
            println("음식을 먹습니다")
        }
    }
    
    class Dog : Runner, Eater {
        override fun run(){
            println("우다다다 뜁니다")
        }
        override fun eat(){
            println("허겁지겁 먹습니다")
        }
    }

!**'여러개'** 의 인터페이스나 클래스에서 같은 이름과 형태를 가진 함수를 구현하고 있다면 서브클래스에서는 혼선이 없도록 필수적으로 **오버라이딩** 할것!


***


# [기본 프로젝트 구조]
## 물리적 구조
### 프로젝트
> _코틀린으로 어플리케이션을 짤 때 관련한 모든 내용을 담는 '큰 틀'_

### 모듈
* 직접 구현한 모듈
* 라이브러리 모듈

모듈은 다수의 폴더와 파일로 이루어짐

코틀린 코드뿐만 아니라 모듈과 관련된 설정 및 리소스 파일 등도 포함될 수 있다.

## 논리적 구조
### 패키지
> _개발시에 소스 코드의 '소속'을 지정하기 위한 논리적 단위_
> _명시하지 않으면 자동으로 'default' 패키지로 묶임_

**명명법** : 개발한 회사의 도메인을 거꾸로 한것 + .프로젝트명 (eg. com.youtube.woowakgood) -> 그 뒤에 기능별로 세분화 (eg. com.youtube.woowakgood.messi)

    package com.youtube.woowakgood
    
    fun main() {
    }
    
코틀린은 자바와 달리 폴더 구조와 패키지 명을 일치시키지 않아도 됨. 단순히 파일 상단에 패키지만 명시하면 컴파일러가 알아서 처리함.

같은 패키지 내에서는 변수 함수 클래스를 공유할 수 있다.


### 패키지 import
> _다른 패키지의 변수 함수 클래스를 사용하기 위해_   
> _이름이 중복되는 것이 있다면 패키지를 포함한 FULL NAME으로 명시해야함_

    package com.youtube.woowakgood
    
    import com.youtube.dogswellfish
    
    fun main() {
    }

코틀린은 자바와 달리 클래스명과 파일명이 일치하지 않아도 되며 하나의 파일에 '여러개의 클래스'를 넣어도 컴파일이 됨

이는 파일이나 폴더를 기준으로 구분하지 않고 파일내에 있는 **package 키워드를 기준** 으로 구분하기 때문!


***


# [변수, 함수, 클래스의 접근범위와 접근제한자]
## 스코프
> _패키지 구조 내에서 변수나 함수, 클래스의 '공용 범위'를 제어하는 단위_   
> _언어차원에서 변수나 함수, 클래스 같은 '멤버'들을 서로 공유하여 사용할 수 있는 범위를 지정해 둔 단위_

eg. 패키지 내부, 클래스 내부, 함수 내부

### 스코프에 대한 세가지 규칙
1. 스코프 외부에서는 스코프 내부의 멤버를 '참조연산자'로만 참조가 가능하다 (eg. dogA.eat())
2. 동일 스코프 내에서는 멤버들을 '공유'할 수 있다
3. 하위 스코프에서는 상위 스코프의 멤버를 재정의 할 수 있다 -> 작은 스코프에서 동일한 이름의 멤버가 나오면 `name shadowed` 경고가 뜨며 작은 스코프에 지정된 변수가 

    val str = "패키지 스코프"
    
    class B{
        val str = "클래스 스코프"
        fun print() { println(str) }
    }
    
    fun main() {
        val str = "함수 스코프"
        println(str)
        B().print()
    }


## 접근제한자
> _스코프 외부에서 스코프 내부에 접근할 때 그 권한을 '개발자가 제어'할 수 있는 기능_   
> _변수 , 함수 , 클래스 선언시 맨 앞에 붙임_

* public
* internal
* private
* protected

### 패키지 스코프에서 접근제한자
* public : **(기본값)** 어떤 패키지에서도 접근 가능
* internal : 같은 모듈 내에서만 접근 가능
* private : 같은 파일 내에서만 접근 가능

### 클래스 스코프에서 접근제한자
* public : **(기본값)** 클래스 외부에서 늘 접근 가능
* private : 클래스 내부에서만 접근 가능
* protected : 클래스 자신과 상속받은 클래스에서 접근 가능


***


# [고차함수와 람다함수]
## 고차함수
> _함수를 마치 클래스에서 만들어낸 '인스턴스처럼' 취급하는 방법_   
> _함수를 '패러미터'로 넘겨 줄 수도 있고 '결과값으로 반환' 받을 수도 있는 방법_   
> _코틀린에서는 모든 함수를 고차함수로 사용 가능_

    fun main(){
        b(::a)
    }

    fun a (str: String) {
        println("$str 함수 a")
    }
    
    fun b (function: (String)->Unit){
        function("b가 호출한")
    }
        
`Unit` : 값이 없다는 형식

`::` : 일반 함수를 고차 함수로 변경해 주는 연산자

근데 넘길때 꼭 함수를 만들어서 넘겨야함? 그래서 나온게 람다함수 ↓

## 람다함수
> _람다함수는 그 자체가 고차함수. 따라서, 별도의 연산자 없이 변수에 담을 수 있다_

    fun main(){
        b(::a)
        
        val c: (String)->Unit = { str -> println("$str 람다함수") } //원래 패러미터의 자료형까지 다 써주는게 맞다.
               //이미 패러미터의 자료형이 기술되어 있어 자료형이 자동으로 추론되므로 str: String 에서 자료형은 생략가능하다.
        b(c)
    }

    fun a (str: String) {
        println("$str 함수 a")
    }
    
    fun b (function: (String)->Unit){
        function("b가 호출한")
    }

`val a: Int` 일반적인 자료형을 쓴것처럼 `val a: (String)->Unit` 그 자리에 함수의 형식을 쓴것

### 타입추론을 이용한 람다함수 축약
`val c: (String)->Unit = { str -> println("$str 람다함수") }` ----> `val c = { str:String -> println("$str 람다함수") }`

### 람다함수의 특별한 케이스들
* 람다함수도 여러 구문의 사용이 가능 -> **마지막 구문의 결과값** 이 '반환'됨
    val a: (Int, Int)->Int = { a,b ->
        println("여러줄")
        println("쌉가능")
        a+b }
        
* 패러미터가 없는 람다함수는 실행할 구문들만 나열하면 됨
    val a = {println("패러미터가 없듬")}
* 패러미터가 하나뿐이라면 `it` 사용
    val a: (String)->Unit = {"$it 발테리 잇츠 제임스"}


***

# [스코프함수]
> _함수형 언어의 특징을 좀 더 편리하게 사용할 수 있도록 기본 제공하는 함수들_   
> _main함수와 '별도의 scope'에서 인스턴스의 변수와 함수를 조작하므로 코드가 깔끔해지는 장점_

?클래스에서 생성한 인스턴스를 스코프 함수에 전달하면 인스턴스의 속성이나 함수를 스코프 함수 내에서 더 편하게 사용할 수 있도록 하는 기능?

인스턴스의 속성이나 함수를 scope 내에서 깔끔하게 분리하여 사용할 수 있다는 점 때문에 코드의 가독성을 향상시킨다는 장점

* apply
* run
* with
* also
* let

### apply
> 인스턴스를 생성한 후 변수에 담기 전에 '초기화 과정'을 수행할 때 많이 사용
> '인스턴스 자신'을 다시 반환

    fun main() {
        var a = Book("물먹는법특강", 30000).apply{
            name = "[초한정판]" + name
            discount()
        }
    }

    class Book(var name:String, var price:Int){
        fun discount(){
        price -= 2000
        }
    }
    
람다함수 형식으로 참조연산자 없이 바로 사용

인스턴스 자신을 다시 반환하므로 생성되자마자 조작된 인스턴스를 변수에 바로 넣어줄 수 있다.

### run
> 이미 인스턴스가 만들어진 후에 인스턴스의 함수나 속성을 스코프 내에서 사용할 때 유용   
> '마지막 구문'을 반환

    var b = a.run{
        println(a.prince)
        a.name
    }


    fun main() {
        var a = Book("물먹는법특강", 30000).apply{
            name = "[초한정판]" + name
            discount()
        }
        
        a.run{
            println("상품명 : ${name}, 가격 : ${price} 원")
        }
    }

    class Book(var name:String, var price:Int){
        fun discount(){
        price -= 2000
        }
    }
    
### with
> run과 동일한 기능, 단지 인스턴스를 참조연산자 대신 '패러미터'로 받는다는 차이

`a.run{...}` -> `with(a){...}`


### also 와 let
apply/also 는 처리가 끝나면 '인스턴스'를 반환

run/let 은 처리가 끝나면 최종값을 반환

apply, run 과의 차이점으로는 **also** , **let** 은 마치 패러미터로 인스턴스를 넘긴것처럼 `it`을 통해서 인스턴스를 사용할 수 있다.

**이유** : 같은 이름의 변수나 함수가 **'scope 바깥에 중복'**  되어 있는 경우에 혼란을 방지하기 위함

    fun main() {
        var price = 5000
    
        var a = Book("물먹는법특강", 30000).apply{
            name = "[초한정판]" + name
            discount()
        }
        
        a.run{
            println("상품명 : ${name}, 가격 : ${price} 원")
        }
    }

    class Book(var name:String, var price:Int){
        fun discount(){
        price -= 2000
        }
    }

-> `상품명 : [초한정판]물먹는법특강, 5000 원` **price라는 변수가 중복!**


    fun main() {
        var price = 5000
    
        var a = Book("물먹는법특강", 30000).apply{
            name = "[초한정판]" + name
            discount()
        }
        
        a.let{
            println("상품명 : ${it.name}, 가격 : ${it.price} 원")
        }
    }

    class Book(var name:String, var price:Int){
        fun discount(){
        price -= 2000
        }
    }
    
-> `상품명 : [초한정판]물먹는법특강, 28000 원`


***


# [오브젝트]
> _생성자 없이 객체를 직접 만들어 냄_   
> _단 하나의 객체만으로 공통적인 속성과 함수를 사용해야하는 코드에서 사용_   
> _ **Singleton Pattern** 을 언어차원에서 지원!!_

기존의 클래스는 내부에 있는 속성이나 함수를 사용하려면 '생성자'를 통해 실체가 되는 인스턴스 객체를 만들어야 한다.

오브젝트는 그 자체로 객체이기 때문에 생성자는 사용하지 않음.

오브젝트로 선언된 객체는 '최초 사용 시' 자동으로 생성되고, 이후에는 코드 전체에서 '공용으로 사용'될 수 있기 때문에 프로그램이 종료되기 전까지 공통적으로 사용할 내용들을 믂어 만드는 것이 좋다.

    fun main(){
        println(Counter.count)
        
        Counter.countUp()
        Counter.countUp()
        
        println(Counter.count)
        
        Counter.clear()
        
        println(Counter.count)
    }
    
    object Counter {
        var count = 0
        
        fun countUp(){
            count++
        }
        
        fun clear(){
            count = 0
        }
    }
    
## Companion Object
> _클래스 안에 오브젝트 사용_   
> _인스턴스간의 서로 공용 속성 및 함수로 사용_   
> _기존의 언어들의 Static 멤버와 비슷_

    fun main(){
        var a = FoodPoll("짜장")
        var b = FoodPoll("짬뽕")
        
        a.vote()
        a.vote()
        
        b.vote()
        b.vote()
        b.vote()
        
        println("${a.name} : ${a.count}")
        println("${b.name} : ${b.count}")
        println("총계 : ${FoodPoll.total}")
    }
    
    class FoodPoll (val name: String){
        companion object{
            var total = 0
        }
        var count = 0
        
        fun vote(){
            total++
            count++
        }
    }


***


# ☆☆☆ [익명객체와 옵저버 패턴] ☆☆☆ 20.08.23 많이 어렵다 다시 제대로 이해하고 넘어
## 옵저버 패턴
> '이벤트가 일어나는 것을 감시'하는 감시자의 역할

e.g. 안드로이드 : 키의 입력, 터치의 발생, 데이터의 수신등 함수로 직접 요청하지 않았지만 시스템 또는 루틴에 의해 발생하게 되는 동작들을 '이벤트' 라고 부르며 이 '이벤트' 가 발생할 때 마다 '즉각적으로 처리' 할 수 있도록 만드는 프로그래밍 패턴을 '옵저버 패턴' 이라고 부른다.

### 옵저버 패턴의 구조
* 이벤트를 수신하는 클래스 : A 라고 지칭
* 이벤트의 발생 및 전달하는 클래스 : B 라고 지칭

A에 B의 인스턴스를 생성하여 사용하기 때문에 A는 B를 직접 참조할 수 있지만 반대로 B는 A를 참조할 수 없기때문에 사이에 **인터페이스** 를 끼워넣음.

이 인터페이스를 **'observer'** , 코틀린에서는 **'listener'** 라고 함.

이렇게 이벤트를 넘겨주는 행위를 **'callback'** 이라고 함.

_리스너를 통해 이벤트를 반환하는 함수 이름은 관례적으로 `on(행위)` 라는 규칙을 따름_

    fun main(){
        EventPrinter().start()
    }
    
    interface EventListener{
        fun onEvent(count: Int)
    }
    
    class Counter(var listener: EventListener){
        fun count(){
            for(i in 1..100){
                if(i % 5 == 0) listener.onEvent(i)
            }
        }
    }
    
    class EventPrinter: EventListener{
        override fun onEvent(count: Int){
            print("${count}-")
        }
        
        fun start(){
        //this는 EventPrinter 객체 자신을 나타내지만 받는 쪽에서 'EventListener'만 요구했기 때문에 EventListener 구현부만 넘겨주게 됨
        //이를 객체지향의 다형성이라고 함
            val counter = Counter(this) 
            counter.count()
        }
    }
    
## 익명객체
> _오브젝트와의 차이는 이름이 없다는 점_   
> _인터페이스를 구현한 객체를 코드 중간에도 '즉시 생성'하여 사용할 수 있음_

    fun main(){
        EventPrinter().start()
    }
    
    interface EventListener{
        fun onEvent(count: Int)
    }
    
    class Counter(var listener: EventListener){
        fun count(){
            for(i in 1..100){
                if(i % 5 == 0) listener.onEvent(i)
            }
        }
    }
    
    class EventPrinter{
        fun start(){
        // Counter(익명객체) 형식임. 저 긴 문장이 익명함수로 넘길 패러미터 단 한 개.
            val counter = Counter(object: EventListener{
                override fun onEvent(count: Int){
                    print("${count}-")
                }
            })
            counter.count()
        }
    }


참고로 위의 익명객체에서 오버라이드 해야할 함수가 하나면 좀더 간단하게 구현 가능 -> **람다함수** 이용? -> 한번해볼것 20-08-25

안드로이드에서 자바로 되어있는 인터페이스? 를 사용할때만 코틀린으로 SAM 방식?으로 람다함수 이용가능

순수하게 코틀린으로 할때는 그냥 이렇게 넘기면 된다고 함.
    
    
***


# [클래스의 다형성]

**수퍼클래스** : 음료클래스 (Drink)

**서브클래스** : 콜라클래스 (Coke)

* **Up-Casting** : 하위 자료형을 상위 자료형인 수퍼클래스로 변환 `var a: Drink = Coke()`
* **Down-Casting** : Up-Casting 된 인스턴스를 다시 하위 자료형으로 변환. **별도의 연산자** 필요

### Down-Casting 연산자

* `as` : '변수'를 호환되는 자료형으로 변환해주는 캐스팅 연산자
    var a: Drink = Coke()
    a as Coke // 즉시 자료형 변환

    var a: Dring = Coke()
    var b = a as Coke // 변환된 결과를 반환해주고 **a 변수 자체도 다운캐스팅** 됨

* `is` : 변수가 자료형에 호환되는지를 먼저 **'체크한 후 변환'** 해주는 캐스팅 연산자. 조건문에서 사용하며 그 **조건문 내에서만** 캐스팅
    var a: Drink = Coke()
    if(a is Coke){
        // **이 안에서만 a가 Coke가 됨**
    }
    



***



# 제너릭 정의 정확하게 다시 설명한거 찾아서 적어놓을 수 있도록 20/08/27
# [제너릭]
> _클래스나 함수에서 사용하는 자료형을 외부에서 지정할 수 있는 기능_   
> _캐스팅 연산을 거치는 것은 프로그램의 속도를 저하시킬 수 있다는 단점 때문에 나온 제너릭_


제너릭은 함수나 클래스를 선언할 때 고정적인 자료형 대신 실제 자료형으로 대체되는 **'타입 패러미터'** 를 받아 사용하는 방법

`<T>` 이 타입 패러미터에 특정 자료형이 할당되면 `T` 제너릭을 사용하는 모든 코드는 할당된 자료형으로 대체되어 컴파일 됨.

`fun <T> genericFunc(param: T): T` -> `fun <Int> genericFunc(param: Int) Int`

`class GenericClass <T> (var pref: T)` -> `class GenericClass <Int> (var pref: Int)`

따라서, 캐스팅 연산없이도 자료형을 그대로 사용할 수 있다..?

`<T>` 타입패러미터의 이름은 클래스 이름과 규칙이 같지만 일반적으로 'Type'의 이니셜인 'T' 를 사용하는것이 관례

여러개의 제너릭을 사용할 경우 'T' 의 다음 알파벳인 'U'와 'V'를 사용하기도 함. `<T,U,V>`

제너릭을 특정한 수퍼 클래스를 상속받은 클래스 타입으로만 제한하려면 `<T: SuperClass이름>`

## 사용법?
### 함수에 제너릭을 선언한 경우
`fun <T> genericFunc (var param: T){}`   

`genericFunc(1)` 처럼 일반적인 함수처럼 사용하면 패러미터나 반환형을 통해 타입 패러미터를 통해 자동으로 추론

### 클래스의 경우
`class GenericClass <T>`   
`GenericClass<Int>()` 인스턴스를 생성할때 타입 패러미터를 수동으로 지정하거나 `<Int>`   

`class GenericClass <T> (var pref: T)`   
`GenericClass(1)` 생성자에 제너릭이 사용된 경우 지정하지 않아도 자동으로 추론

### 제너릭 예제
    fun main(){
        UsingGeneric(A()).doShouting()    //UsingGeneric<A>(A()).doShouting() 이렇게 타입패러미터를 수동으로 전달할 수도 있지만 추론가능하므로 생략
        UsingGeneric(B()).doShouting()
        UsingGeneric(C()).doShouting()
    }
    
    open class A {
        open fun shout(){
            println("A가 사자후")
        }
    }
    
    class B : A(){
        override fun shout(){
            println("B와 사자후")
        }
    }
    
    class C : A(){
        override fun shout(){
            println("C는 사자후")
        }
    }
    
    class UsingGeneric <T:A> (val t: T){
       fun doShouting(){
           t.shout()
       }
    }

**여기서 제너릭을 사용하지않고 UsingGeneric의 생성자에서 수퍼클래스인 A로 캐스팅하여 shout을 호출하여도 동작은 같겠지만**   
**이렇게 제너릭을 사용하는 경우 사용할 때 제너릭이 자료형을 대체하게 되어 캐스팅을 방지할 수 있으므로 성능을 더 높일 수 있다..?**   
`class UsingGeneric(val t:A)` -> `calss UsingGeneric <T:A> (val t:T)`

### 제너릭을 함수 사용하는법
    fun main(){
        doShouting(A())
    }
    
    fun <T:A> doShouting(t:T){
        t.shout()
    }
    
    open class A {
        open fun shout(){
            println("A가 사자후")
        }
    }

**제너릭에 대한 자세한 얘기는 나중 강의에서 설명해준다 함**



***


# [리스트]
> _데이터를 코드에서 지정한 순서대로 저장해두는 리스트_   

리스트는 '데이터를 모아 관리'하는 Collection 클래스를 상속받는 서브 클래스 중 가장 단순한 형태 중 하나로   
여러개의 데이터를 원하는 순서로 넣어 관리하는 형태


### 리스트의 종류 2가지
* List<out T>    :    생성시에 넣은 객체를 대체, 추가, 삭제 할 수 없음
* MutableList<T>    :    생성시에 넣은 객체를 대체, 추가, 삭제가 가능함

### 리스트를 생성하는 방법
전용함수 사용   
* `listOf(1,2,3)`
* `mutableListOf("A","B","C")`

### MutableList의 함수
* `add(데이터)`
* `add(인덱스, 데이터)`
* `remove(데이터)`
* `removeAt(인덱스)`
* `shuffle()`
* `sort()`
* `list[인덱스] = 데이터`


***


# [문자열을 다루는 법]
> _String 클래스와 관련된 여러 속성과 함수_   
> _그 중 자주쓰이는것 설명_

### 주로 사용하는 속성과 함수
* `length` : 문자열의 길이 속성(Int 타입)
* `toLowerCase()` : 영문 소문자로 문자열 전체 변환하여 반환 -> 해당 문자열에 바로 적용되는 것은 아님
* `toUpperCase()` : 영문 대문자로 문자열 전체 변환하여 반환 -> 해당 문자열에 바로 적용되는 것은 아님
* `split("delimiter")` : delimiter를 기준으로 문자열을 나누어 문자열 배열로 반환 -> **자바와 달리 split에 정규식이 아닌 일반 문자열을 넣어도 동작**
* `joinToString()` : 문자열 배열을 합쳐서 반환함? -> 정확히 어떤걸 합쳐서 문자열로 반환한다는거지?
* `joinToString("문자열")` : 지정한 문자열을 사이에 넣어서 합쳐서 반환함? -> 얘도마찬가지
* `substring(5..10)` : for문에서 사용했었던 **IntRange** 형식을 사용하여 시작과 끝을 정해주어 그 부분만 반환

### 문자열이 비어있는지 여부를 판단하여 boolean 값으로 반환받는 함수
* `isNullOrEmpty()` : null 이거나 empty면 true를 반환 -> null 이거나 아예 비어야함
* `isNullOrBlank()` : null 이거나 blank면 true를 반환 -> null 이거나 공백문자만 있어아햠 (Space, Tab, Line Feed, Carrige Return 등등)

    fun main() {
        val nullString: String? = null
        val emptyString = ""
        val balnkString = " "
        val normalString = "A"
    }

### 특수한 함수들
* `startsWith("문자열")` : 지정한 문자열로 시작하면 true를 반환
* `endsWith("문자열")` : 지정한 문자열로 끝나면 true를 반환
* `contains("문자열")` : 지정한 문자열을 포함하면 true를 반환


***


# [null 처리와 동일성의 확인]
> _nullable 변수에서 null을 처리하는 법과_   
> _변수 간에 동일성을 확인하는 법_

## null 처리
null 상태로 속성이나 함수를 쓰려고 하면 null pointer exception이 발생하기 때문에 nullable 변수를 사용할 때에는 null check 없이는 코드가 컴파일되지 않는다.   
null check를 하기위해 일일히 if문으로 조건을 체크하는 대신 다른 방법을 사용.

* `?.` : null safe operator
* `?:` : elvis operator
* `!!.` : non-null assertion operator

### null safe 연산자
참조연산자를 실행하기 전에 먼저 객체가 null인지 확인부터하고 객체가 null 이라면 **뒤따라오는 구문을 실행하지 않는** 연산자   
`sample?.toUpperCase()` -> sample이 null이라면 toUpperCase()는 실행되지 않는다

### elvis 연산자
객체가 null이 아니라면 그대로 사용하지만 null 이라면 **연산자 우측의 객체로 대체** 되는 연산자   
`sample?:"default"` -> sample이 null이라면 대신 "default" 문자열을 사용

### non-null assertion 연산자
~참조연산자를 사용할 때 null 여부를 컴파일 시 확인하지 않도록 하여 **런타임 시 null pointer exception이 나도록 의도적으로 방치** 하는 연산자~   
null이 아님을 직접 명시해주는 연산자   
non-null 타입의 패러미터를 요구하는 함수에 넘겨주려는 데이터가 nullable 타입이면 넘겨줄 수 없음.   
따라서, 넘겨주려는 데이터가 non-null 임을 보장할 수 있으면 !!. 을 써서 null이 아님을 명시해서 넘겨줌.   
**!의도적으로 명시하는 것이므로 null pointer exception이 발생할 수 있으므로 조심해서 사용할것!**

### 예제
    fun main(){
        var a: String? = null
        println(a?.toUpperCase())
        println(a?:"default".toUpperCase())
        println(a!!.toUpperCase())
    }
->   
`null`   
`DEFAULT`   
`null pointer exception`

### 스코프 함수와 함께 사용하면 더욱 편리
**!null을 체크하기 위해 if문 대신 사용하면 더욱 편리!**

    fun main(){
        var a: String? = null
        var b: String? = "BaBo"
        a?.run{
            println(toUpperCase())
            println(toLowerCase())
        }
        b?.run{
            println(toUpperCase())
            println(toLowerCase())
        }
    }
    
## 변수의 동일성 체크

* **내용의 동일성** : 메모리상에 서로 다른곳에 할당된 객체라도 **그 내용이 같다면 동일** 하다고 판단하는 것
* **객체의 동일성** : 서로 다른 변수가 **메모리상에 같은 객체를 가르킬때만 동일** 하다고 판단하는 것

내용의 동일성을 판단하는 연산자 `==`   
객체의 동일성을 판단하는 연산자 `===`

!'내용의 동일성'은 자동으로 판단되는 것이 아닌 코틀린의 모든 클래스가 내부적으로 상속받는 'Any' 라는 최상위 클래스의 `equals()` 함수가 반환하는 Boolean 값으로 판단!

기본 자료형에는 자료형의 특징에 따라 equals() 함수가 이미 구현되어 있지만 커스텀 class를 만들때는 `open fun equals(other: Any?):Boolean` equals 함수를 상속받아   
동일성을 확인해주는 구문을 **별도로 구현해야 함**

### 예제
    fun main(){
        var a = Product("코카콜라", 1000)
        var b = Product("코카콜라", 1000)
        var c = a
        var d = Product("펩시", 990)
        
        println(a == b)
        println(a === b)
        
        println(a == c)
        println(a === c)
        
        println(a == d)
        println(a === d)
    }
    
    class Product(val name: String, val price: Int){
        override fun equals(other: Any?): Boolean{
            if(other is Product){
                return other.name == name && other.price == price
            } else {
                return false
            }
        }
    }
    
    
***

# [함수의 다양한 기능]
> 함수의 argument를 다루는 방법과 infix 함수

## overloading
> _'같은 Scope 안'에서 같은 이름의 함수를 여러개 만들 수 있는 기능_   
> _함수의 이름이 같더라도 패러미터의 자료형이 다르거나 개수가 다르다면 서로 다른 함수로 동작_   
> _(패러미터의 이름만 다르고 자료형의 갯수나 타입이 동일하면 안됨)_

## default arguments
> _패러미터를 받아야 하는 함수지만 별다른 패러미터가 없더라도 기본값으로 동작할 수 있게해줌_

`deliveryItem(name: String, count: Int=1, destination: String = "집"){}`

## named arguments
> _위의 예제에서 이름과 목적지만 넣고 갯수는 기본값을 이용하고싶을때_   
> _패러미터의 순서와 관계없이 패러미터의 이름을 사용하여 직접 패러미터의 값을 할당하는 기능_

`deliveryItem("선물", destination = "친구집")`

## variable number of arguments (vararg)
> _같은 자료형을 개수 상관없이 패러미터로 받고 싶을 때 사용하는 기능_   
> _마치 배열처럼 참조할 수 있다_   
> **!개수가 지정되지 않은 패러미터라는 특징 때문에 다른 패러미터와 같이 쓸때는 반드시 맨 마지막에 위치!**

    fun main(){
        sum(1,2,3,4)
    }

    fun sum(vararg numbers: Int){
        var sum = 0
        for(n in numbers){
            sum += n
        }
        print(sum)    
    }
    
## infix function 설명이 매우 부족 설명이 매우 부족 설명이 매우 부족 설명이 매우 부족
> _마치 연산자처럼 쓸수있는 함수? 설명이 매우 부족_

    fun main(){
        println(6 multiply 4)
        println(6.multiply(4))
    }

    infix fun Int.multiply(x: Int): Int = this * x
    
class 내에서 infix함수를 선언할 때에는 적용할 클래스가 자기 자신이므로 클래스 이름은 쓰지 않는다   
e.g. : `infix fun multiply(x: Int): Int = this * x`


***


# [중첩클래스와 내부클래스]
> _클래스 안에 클래스가 중첩되는 두 가지 유형의 클래스_   
> _클래스간의 연계성을 표현하여 코드의 가독성 및 작성 편의성이 올라간다..?_

## 중첩클래스(Nested Class)
> _하나의 클래스가 다른 클래스의 기능과 강하게 연관되어 있다는 의미를 전달하기 위해 만들어진 형식_   
> _코드의 형태만 내부에 존재할 뿐 실질적으로는 서로 내용을 직접 공유할 수 없는 별개의 클래스_

    class Outer{
        class Nested{
        }
    }
    
사용할 때는 외부클래스이름.중첩클래스이름 `Outer.Nested()`   
이때 중첩클래스 대신 내부클래스라는 것을 사용할 수 있다.

## 내부클래스
> _혼자서 객체를 만들 수는 없고 외부 클래스의 객체가 있어야만 생성과 사용이 가능한 클래스_   
> _외부클래스 객체 안에서 사용되는 클래스 이므로 외부 클래스의 속성과 함수의 사용이 가능_

    class Outer{
        var text = "Outer Class"
        inner class Inner{
            var text = "Inner Class"
            fun introOuter(){
                println(this@Outer.text)    //외부클래스와 내부클래스에 같은 이름의 속성이나 함수가 있다면 외부클래스의 속성,함수는 'this@OuterClass이름' 으로 참조
            }
        }
    }


***


# [특별한 유형의 클래스]
> _Data Class 와 Enum Class_

## Data Class
> _데이터를 다루는 데에 최적화된 class_   
> _5가지 기능을 내부적으로 자동으로 생성_

**사용자가 직접 호출하기 위한 함수가 아닌 배열이나 리스트 등의 데이터 클래스에 객체가 담겨있을때 이 내용을 자동으로 꺼내 쓸 수 있는 기능을 지원하기 위한 함수들**

1. `equals()` : 내용의 동일성을 판단하는
2. `hashcode()` : 객체의 내용에서 고유한 코드를 생성하는
3. `toString()` : 포함된 속성을 보기쉽게 나타내는
4. `copy()` : 객체를 복사하여 똑같은 내용의 새 객체를 만드는
    똑같은 내용의 객체를 생성할 수 있지만 패러미터를 줘 일부 속성을 변경할 수도 있다.
    val a = Data("A",7)
    val b = a.copy()
    val c = a.copy("B")
5. `componentX()` : 속성을 순서대로 반환하는
    Data("A", 7) 에서 "A"가 component1(), 7이 component2()

### 예제
    fun main(){
        val a = General("A",1)
        println(a == General("A",1)
        println(a.hashcode())
        println(a)
        
        val b = Data("B",2)
        println(b == Data("B",2))
        println(b.hashcode())
        println(b)
        
        println(b.copy())
        println(b.copy("C"))
        println(b.copy(3))
    }
    class General(val name: String, val id: Int)
    data class Data(val name: String, val id: Int)


**for문의 내부적으로는 a에 component1(), b에 component2() 함수를 사용해 순서대로 값을 불러옴**

    fun main(){
        val list = listOf(Data("A",1),
                        Data("B",2),
                        Data("C",3))
        for((a,b) in list){    // 내부적으로는 a에는 component1()이 b에는 component2()라는 함수를 사용하여 순서대로 값을 불러옴
            println("${a}, ${b}")
        }
    }
    class General(val name: String, val id: Int)
    data class Data(val name: String, val id: Int)

## Enum Class (enumerated type : 열거형)
> _enum class 내에 상태를 구분하기 위한 객체들을 이름을 붙여 여러개 생성해두고_   
> _그 중 하나의 상태를 선택하여 나타내기 위한 클래스_

enum class 내의 객체들은 관행적으로 대문자로 기술 (e.g. Color.RED)   
enum의 객체들은 고유한 속성을 가질 수 있음   
일반 클래스처럼 함수도 추가할 수 있음 (객체의 선언이 끝나는 위치에 세미콜론을 추가한 후 함수를 추가하면 됨)

    enum class Color(val number: Int){
        RED(1),
        BLUE(2),
        GREEN(3);
        
        fun isRed() = this == Color.Red
    }

### 예제

    fun main(){
        var state = State.SING    //enum은 선언시에 만든 객체를 이름으로 참조하여 그대로 사용하게 됨
        println(state)
        
        state = State.SLEEP
        println(state.isSleeping())
        
        state = State.EAT
        println(state)
    }
    
    enum class State(val message: String){
        SING("노래함"),
        EAT("밥먹음"),
        SLEEP("잠을잠");
        
        fun isSleeping() = this == State.SLEEP
    }


***


# [컬렉션 Set과 Map]
> _Collection 클래스중 List, Set, Map_

## Set
> _Set은 List와 달리 순서가 정렬되지 않으며 중복이 허용되지 않는 컬렉션 (집합이니까)_   
> _따라서 인덱스로 위치를 지정하여 객체참조 불가 (대신 contains 사용)_

List와 마찬가지로 객체의 추가 삭제가 가능한지 여부에 따라   
* Set<out T>
* MutableSet<T>
 
* `add(데이터)` : 추가
* `remove(데이터)` : 삭제
* `contains` 로 객체가 set 안에 있는지 확인

## Map
> _Key,Value 쌍으로 넣어주는 컬렉션_   
> _객체의 위치가 아닌 고유한 key를 통해 객체를 참조_

내부적으로는 `MutableMap.MutableEntry` 에 key, value 객체로 담겨져 있음   
* key : 객체를 찾기위한 값
* value : key와 연결된 객체

마찬가지로 객체의 추가 삭제가 가능한지 여부에 따라   
* Map<K, out V>
* MutableMap<K, V>

* `put(키,값)` : 요소의 추가
* `remove(키)` : 요소의 삭제

### 예제
key와 value를 `to`로 이어줌

    fun main(){
        val a = mutableMapOf("레드벨벳" to "음파음파",
                            "트와이스" to "FANCY",
                            "ITZY" to "Not Shy")
        for(entry in a){
            println("${a.key} : ${a.value}")    //앞서서 MutableMap.MutableEntry에 key와 value로 있다고 했으므로 이렇게 출력가능
        }
        
        println(a["레드벨벳"])
    }


***


# [컬렉션 함수]
> _list나 set,map과 같은 컬렉션 또는 배열에 일반 함수 또는 람다 함수 형태를 사용하여_   
> _for문 없이도 아이템을 순회하며 참조하거나 조건을 걸고, 구조의 변경까지 가능한 여러가지 함수_   

`for(item in collection)` for문 말고도 **코틀린의 함수형 언어의 특징을** 활용해 컬렉션 사용   
반복문과 조건문을 사용하는 경우를 대부분 대체할 수 있다는 장점

* forEach : `collection.forEach{}` 중괄호 안에서 collection의 객체들을 `it` 이라는 변수로 순서대로 참조 가능
* filter : `collection.filter{it<4}` 중괄호 안의 조건에 맞는collection의 객체들만 반환
* map : `collection.map{it*2}` 중괄호 안의 수식을 collection의 객체들에 적용해 반환
* any : `collection.any{it == 0}` 하나라도 조건에 맞으면 true
* all : `collection.all{it == 0}` 모두 조건에 맞으면 true
* none : `collection.none{it == 0}` 하나도 조건에 맞지 않으면 true
* first (일반함수) : `collection.first()` 컬렉션의 첫번째 아이템 반환
* first (람다함수) : `collection.first{it>3}` 조건에 맞는 첫번째 아이템을 반환 -> **find로 대체가능**
* last (람다함수) : `collection.last{it>3}` 조건에 맞는 마지막 아이템을 반환 -> **findLast로 대체가능**

first , last 사용할때 조건에 맞는 객체가 없는경우(=컬렉션이 비어있는 경우) 문제발생 -> NoSuchElementException
* firstOrNull : 조건에 맞는 객체가 없는경우 null을 반환
* lastOrNull : 조건에 맞는 객체가 없는경우 null을 반환

* count (일반함수) : `collection.count()` 컬렉션의 모든 아이템의 개수 반환
* count (람다함수) : `collection.count{it>7}` 조건에 맞는 아이템의 개수 반환

* associateBy : `collection.associateBy{it.name}` 객체에서 key를 추출하여 map으로 변환하는 함수   
<img src="/Kotlin/image/associateBy.png" width="40%" height="40%" title="px(픽셀) 크기 설정" alt="associateBy"></img>

* groupBy : `collection.groupBy{it.birthYear}` key가 같은 아이템끼리 배열로 묶어 map으로 만드는 함수   
<img src="/Kotlin/image/groupBy.png" width="40%" height="40%" title="px(픽셀) 크기 설정" alt="groupBy"></img>

* partition : `collection.partition{it.birthYear>2002}` 아이템에 조건을 걸어 **두 개의 컬렉션** 으로 나누어 줌   
<img src="/Kotlin/image/partition.png" width="40%" height="40%" title="px(픽셀) 크기 설정" alt="partition"></img>   
**두 컬렉션은 두 객체를 담을 수 있는 'Pair'라는 클래스 객체로 반환되므로 각각의 컬렉션을 'first' , 'second'로 참조하여 사용**   
**또는 페어를 직접 받아줄 수 있도록 변수이름을 괄호안에 두 개 선언해주면 각각의 변수 이름으로 받을 수 있다**   
`val(over2002, under2002) = collection.partition{it.birthYear>2002}`

* flatMap : `collection.flatMap{listOf(it*3,it+3)}` 아이템마다 만들어진 컬렉션을 합쳐서 반환하는 함수
* getOrElse : `collection.getOrElse(1){50}` 인덱스 위치()에 아이템이 있으면 아이템을 반환하고 아닌 경우 지정한 기본값{}을 반환하는 함수
* zip : `collectionA zip collectionB` 컬렉션 두 개의 아이템을 1:1로 매칭하여 새 컬렉션을 만들어 줌   
**1:1로 매칭하여 pair클래스의 객체로 만든후 list에 넣어 반환**  
**이때 반환된 결과 list의 아이템의 개수는 더 작은 컬렉션을 따라가게 됨**


***


# [변수의 고급기술]

`var` 은 할당된 객체를 변경 가능   
`val` 은 할당된 객체를 변경 불가능 **BUT** 객체 내부의 속성은 변경할 수 있으니까 오해말것

## 상수
> _컴파일 시점에 결정되어 절대 바꿀 수 없는 값_   
> _의례적으로 대문자와 언더바만 사용함_

`val` 앞에 `const`를 붙여 선언   
`const val CONST_A = 1`

상수로 선언할 수 있는 자료형은 **기본 자료형** 만 가능 (String 포함)   
런타임에 생성될 수 있는 일반적인 다른 클래스의 객체들은 담을 수 없음   
클래스의 속성이나 지역변수등으로는 사용할 수 없음   
반드시 **companion object 안에** 선언하여 객체의 생성과 관계없이 클래스와 관계된 고정적인 값으로만 사용하게 됨   

변수와의 성능적인 차이로는 변수는 런타임시 객체를 생성하는데 시간이 더 소요됨   
따라서 늘 고정적으로 사용할 값은 상수를 통해 객체의 생성없이 메모리에 값을 고정하여 사용

### 예제
    fun main(){
        foodCourt().searchPrice(FoodCourt.FOOD_PASTA)
    }
    
    class FoodCourt{    //사람들이 무슨음식이 있는지 모르므로 이런식으로 사용을 많이 함
        fun searchPrice(foodName: String){
            val price = when(foodName){
                FOOD_PAST -> 20000
                FOOD_STEAK -> 50000
                FOOD_PIZZA -> 30000
                else -> 0
            }
            
            println("${foodName} : ${price}원.")
        }
        
        companion objecet {
            const val FOOD_PASTA = "파슷하"
            const val FOOD_STEAK = "스텎끼"
            const val FOOD_PIZZA = "핏짜"
        }
    }

## lateinit
> _일단 변수만 선언하고 초기값의 할당은 나중에 할 수 있도록 하는 키워드_

코틀린에서는 변수를 선언할 때 객체를 바로 할당하지 않는 경우에는 기본적으로 컴파일이 되지 않음   
경우에 따라 변수에 객체를 할당하는게 선언과 동시에 할 수 없을 때도 있음

`lateinit var text: String`

**lateinit var 변수의 제한사항**   
초기값 할당 전까지 변수를 사용할 수 없음 (에러발생)   
기본 자료형에는 사용할 수 없음 **(String 클래스에는 사용 가능)**

`::a.isInitialized` : lateinit 변수의 초기화 여부 확인

### 예제
    fun main(){
        val a = LateInitSample()
        
        println(a.getLateInitText())
        a.text = "바보"
        println(a.getLateInitText())
    }
    
    class LateInitSample{
        lateinit var text: String
        
        fun getLateInitText(): String{
            if(::text.isInitialized){
                return text
            }else{
                return "기본값"
            }
        }
    }
    
## lazy
> _변수를 사용하는 시점까지 초기화를 자동으로 늦춰주는 지연 대리자 속성(lazy delegate properties)_

lateinit과 달리 **`by`와 람다함수** 형식을 사용   
`val a: Int by lazy{7}`

코드에서는 선언시 즉시 객체를 생성 및 할당하여 변수를 초기화하는 형태를 갖고 있지만   
실제 실행시에는 val 변수를 사용하는 시점에 초기화 과정을 진행하므로써 코드의 **실행시간을 최적화** 할 수 있음   
람다함수로 초기화가 진행되므로 함수안에 여러구문이 들어갈 수 있으며 **맨 마지막 구문의 결과** 가 변수에 할당됨!

### 예제
    fun main(){
        val number: Int by lazy{
            println("초기화를 합니다")
            7
        }
        
        println("시작")
        println(number)
        println(number)
    }
    
    
***


# [비트연산]
> _정수형 변수를 2진법인 비트단위로 연산할 수 있는 기능_

실무에서는 거의 계산에는 사용하지 않으며 (2진법을 이용한 연산 최적화가 필요하다면 컴파일러의 기능을 사용하는 경우가 대부분)   
정수형의 값을 비트단위로 나누어 데이터를 좀 더 작은 단위로 담아 경제성을 높이기 위한 용도로 사용

32비트짜리 Integer 변수에 각각 다른 값을 넣는다거나 / 앞 5비트는 다른값 뒤 27비트는 다른값을 나눠서 넣는다거나   
하는 변수 하나에 여러개의 값을 담아 사용할 수 있음

비트 연산을 사용하는 부하도 무시할 수 없으므로 주로 플래그 값을 처리하거나 (여러개의 상태값을 0과 1로 담는 방법)   
네트워크 등에서 프로토콜의 데이터 양을 줄이기 위해 자주 사용

코틀린은 모든 정수형이 부호를 포함하므로 (부호없는 정수형도 실험 중에 있긴함)   
최상위 비트를 0이면 양수, 1이면 음수인 부호비트로 사용

## bitwise shift operators
* shl(shift left) : 부호비트 제외, 왼쪽 시프트
* shr(shift right) : 부호비트 제외, 오른쪽 시프트
* ushr(unsigned shift right) : 부호비트 포함, 오른쪽 시프트

## bitwise operators
> 원본과 비교대상의 값을 비트 단위로 비교하여 

* and : 비트가 둘다 1인 자리만 1로 반환
* or : 비트가 둘 중 하나라도 1인 자리는 1로 반환
* xor : 비트가 같은 자리는 0, 다른 자리는 1로 반환함

**and** 연산자는 그 특징을 이용해 두가지 기능으로 사용   
* 비트를 확인하는 용도 : 0110 and 0100 -> 2번째 자리의 비트가 1인지 0인지 알아낼 수 있음
* 비트를 clear하는 방법 : 0110 and 1100 -> 하위 두개의 비트를 00으로 clear

**or** 연산자는 비트의 set 연산 비트값을 1로 설정하고 싶을 때 사용   
* 비트를 set : 0110 or 1100 -> 상위 두개의 비트를 1로 set

**xor** 연산자는 비트들이 같은지 비교   
* 비트를 비교 : 0110 xor 1100 -> 같으면 0 다르면 1 이므로 비교가능

## inv()
> _비트를 모두 반전시키는 함수_

## 예제
    fun main(){
        var bitData: Int = 0b10000
        
        bitData = bitData or(1 shl 2)    //1을 좌측으로 2칸 시프트하면 0b100
        println(bitData.toString(2))    //정수형의 경우 toString의 패러미터로 진법 변환을 할 수 있음
        
        var result = bitData and(1 shl 4)
        println(result.toString(2))
        
        println(result shr 4)    //이렇게하면 0b1
        
        bitData = bitData and((1 shl 4).inv())
        println(bitData.toString(2))
        
        println((bitData xor (0b10100)).toString(2))
    }


***


# [코루틴을 통한 비동기 처리]
> _'비동기'로 여러개의 루틴을 동시에 처리할 수 있는 법_   
> _import kotlinx.coroutines.*_

지금까지 모든 구문을 순차적 '동기적'으로 실행했음   
'여러개의 루틴'을 동시에 실행하여 결과를 내고 싶을때? -> 비동기처리를 지원하는 **코루틴**

코루틴은 메인이 되는 루틴과 별도로 진행이 가능한 루틴으로 개발자가 루틴의 실행, 종료를 마음대로 제어할 수 있는 단위

코루틴을 사용할 때는 kotlinx(코틀린익스텐션)의 coroutines 패키지를 전부 임포트해야함 `import kotlinx.coroutines.*`

코루틴은 **제어범위** 및 **실행범위** 를 지정할 수 있음 -> 이를 **코루틴의 Scope** 라고 함

* GlobalScope : 프로그램 어디서나 제어, 동작이 가능한 기본 범위
* CoroutineScope : 특정한 목적의 Dispatcher를 지정하여 제어 및 동작이 가능한 범위 (새로운 coroutine의 범위)

_Dispatcher란? : 아니 그래서 디스패쳐가 뭐냐니깐?   
`Dispatchers.Default` 백그라운드에서 동작하는 디스패쳐   
`Dispatchers.IO` 네트워크나 디스크등 I/O에 최적화된 동작하는 디스패쳐   
`Dispatchers.Main` 메인(UI) 스레드에서 함께 동작하는 디스패쳐_   
이런 Dispatcher들은 모든 플랫폼에서 지원되지는 않으니 조심해서 사용

코루틴은 이러한 Scope에서 제어되도록 생성될 수 있음
    val scope = CoroutineScope(Dispatcher.Default)
    val coroutineA = scope.launch{}
    val coroutineB = scope.async{}
    
* `launch` : 반환값이 없는 Job 객체
* `async` : 반환값이 있는 Deffered 객체 / 마지막 구문의 결과가 반환   
-> 둘 다 람다함수의 형태

코루틴은 제어되는 스코프 또는 프로그램 전체가 종료되면 함께 종료되기 때문에 코루틴이 끝까지 실행되는 것을 보장하려면   
일정한 범위에서 코루틴이 모두 실행될 때까지 잠시 기다려주어야 한다?

* `runBlocking{}` : 코루틴이 종료될 때까지 메인 루틴을 잠시 대기시켜줌
    runBlocking{
        launch{}
        async{}
    }
**주의 : 안드로이드에서는 메인스레드에서 runBlocking을 걸어주면 일정시간이상 응답이 없는 경우**   
**ANR(Application Not Responding)이 발생하며 앱이 강제 종료됨**

### 예제
    import kotlinx.coroutines.*
    
    fun main(){
        val scope = GlobalScope
        
        scope.launch{
            for(i in 1..5){
                println(i)
            }
        }
        
        runBlocking{
            launch{
                for(i in 1..5){
                    println(i)
                }
            }
        }

    }

## 루틴의 대기를 위한 추가적인 함수들
* `delay(milisecond: Long)` : milisecond 단위로 루틴을 잠시 대기시키는 함수
* `join()` `Job.join()` : Job객체에서 호출하여 Job의 실행이 끝날때까지 대기하는 함수
* `await()` `Deferred.await()` : Deferred 객체에서 호출하여 Deferred의 실행이 끝날때까지 대기하는 함수 / **Deferred의 결과도 반환함**

세 함수들은 코루틴 내부 또는 runBlocking{}과 같은 루틴의 대기가 가능한 구문 안에서만 동작이 가능

### 예제
    import kotlinx.coroutines.*
    
    fun main(){
        runBlocking{
            val a = launch{
                for(i in 1..5){
                    println(i)
                    delay(10)
                }
            }
            val b = async{
                "async 종료"
            }
            
            println("async 대기")
            println(b.await())
            
            println("launch 대기")
            a.join()
            println("launch 종료")
            
        }

    }

## 코루틴 실행 도중 중단하는 방법
* `cancel()` : 코루틴에 cancel()을 걸어주면 두 가지 조건이 발생하며 코루틴을 중단시킬 수 있음
1. 코루틴 내부의 delay() 함수 또는 yield() 함수가 사용된 위치까지 수행된 뒤 종료
2. cancel()로 인해 코루틴 내부의 속성인 isActive가 false가 되므로 이를 확인하여 코드를 통해 **수동** 으로 종료

### 예제
    import kotlinx.coroutines.*
    
    fun main(){
        runBlocking{
            val a = launch{
                for(i in 1..5){
                    println(i)
                    delay(10)
                }
            }
            val b = async{
                "async 종료"
            }
            
            println("async 대기")
            println(b.await())
            
            println("launch 대기")
            a.cancel()
            println("launch 종료")
            
        }

    }

## withTimeoutOrNull()
> _제한시간 내에 수행되면 결과값을 아닌 경우 null을 반환_   
> _withTimeoutOrNull(밀리세컨드단위의시간)_   
> **join() 이나 await() 처럼 blocking 함수임!**

    witTimeoutOrNull(50){
        for(i in 1..1000){
            println(i)
            delay(10)
        }
        "Finish"
    }
    
### 예제
    import kotlinx.coroutines.*
    
    fun main(){
        run Blocking{
            var result = withTimeoutOrNull(50){
                for(i in 1..10){
                    println(i)
                    delay(10)
                }
                "Finish"
            }
            println(result)
        }
    }
-> 1 2 3 null
