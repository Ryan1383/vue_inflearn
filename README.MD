## Inflearn Vue 1일차

    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

Vue란 무엇인가?

- MVVM패턴의 뷰모델( viewmodel) 레이어에 해당하는 화면(View) 단 라이브러리
- 이벤트는 ViewModel 의 DOM Listeners가 듣고 javascript의 데이터를 바꿔주거나 특정 로직을 Model에서 실행한다.
- javascript의 data가 변했을 때 ViewModel Data Bindings가 듣고 View에 반영한다.

Vue 컴포넌트

- Vue.compoent('컴포넌트 이름', 컴포넌트내용 ) ; => 전역 컴포넌트
- Vue 인스턴스 내부에 compoents: {'컴포넌트 이름' : 컴포넌트 내용 }
  => 지역컴포넌트

- 전역 컴포넌트는 인스턴스를 생성하지 않아도 모든 인스턴스에 등록 되어있지만 지역컴포넌트는 인스턴스를 생성할 때마다 내부에 생성해줘야한다.

컴포넌트간 통신

- 상위에서 하위로는 data를 내려줌, props 속성
- 하위에서 상위로는 event를 올려줌, event 발생
-       <app-header v-bind:프롭스 속성 이름 = "상위컴포넌트의 데이터이   름"></app-header>
- event \$emit :
  <app-header v-on:하위 컴포넌트에서 발생한 이벤트 이름 ="상위 컴포넌트의 메서드 이름"></app-header>

같은 레벨의 컴포넌트 간의 통신

- 동레벨의 컴포넌트 간의 통신은 공통의 상위컴포넌트를 통해서 event로 올리고 props로 내려주는 방법이 있다.

Vue Router

- https://unpkg.com/vue-router/dist/vue-router.js 를 통한 cdn 스크립트 추가.
- new Router를 사용하여 router 인스턴스를 설정하다. -> Vue 인스턴스 내부에 router속성 추가.
- router 객체의 내부 속성 : {
  routes : routes에는 페이지의 라우팅 정보가 들어간다. ( 어떤 url로 이동하였을 때 어떤 페이지로 이동할지에 대한 배열) 내부에 path component 를 정의
  }
- <router-view>를 사용하여 page 이동을 정한다.
- <router-link to =""> 를 사용하여 페이지 링크 사용 가능
- mode: "history" 는 url 에서 #을 없앤다.

axios를 사용한 통신

- 기존에 data: {} 내부에 있는 값에 접근할 때 this.name 이렇게 접근하였는데 axios를 호출한 후 부터는 this의 값이 데이타를 저장하기 위해 data 속성 안의 값에 접근할 때 this를 사용하면 data속성에 접근할 수 없다.

## Inflearn Vue 2일차

HTTP 프로토콜 요청에 대한 상태

- 2xx - 성공

1.  200 : GET 요청에 대한 성공
2.  204 : No Content. 성공했으나 응답 본문에 데이터가 없음
3.  205 : Reset Content. 성공했으나 클라이언트의 화면을 새로 고침하도록 권고
4.  206 : Partial Conent. 성공했으나 일부 범위의 데이터만 반환

- 3xx -리다이렉션
  : 300번대의 상태 코드는 대부분 클라이언트가 이전 주소로 데이터를 요청하여 서버에서 새 URL로 리다이렉트를 유도하는 경우..

1.  301 : Moved Permanently, 요청한 자원이 새 URL에 존재
2.  303 : See Other, 요청한 자원이 임시 주소에 존재
3.  304 : Not Modified, 요청한 자원이 변경되지 않았으므로 클라이언트에서 캐싱된 자원을 사용하도록 권고. ETag와 같은 정보를 활용하여 변경 여부를 확인

- 4xx - 클라이언트 에러
  : 400번대 상태 코드는 대부분 클라이언트의 코드가 잘못된 경우이다. 유효하지 않은 자원을 요청했거나 요청이나 권한이 잘못된 경우 발생한다. 요청한 자원이 서버에 없다는 의미.

1.  400 : Bad Request, 잘못된 요청
2.  401 : Unauthorized, 권한 없이 요청. Authorization 헤더가 잘못된 경우
3.  403 : Forbidden, 서버에서 해당 자원에 대해 접근 금지
4.  405 : Method Not Allowed, 허용되지 않은 요청 메서드
5.  409 : Conflict, 최신 자원이 아닌데 업데이트하는 경우. ex) 파일 업로드 시 버전 충돌

- 5xx - 서버에러 = 서버 쪽에서 오류가 난 경우

1.  501 : Not Implemented, 요청한 동작에 대해 서버가 수행할 수 없는 경우
2.  503 : Service Unavailable, 서버가 과부하 또는 유지 보수로 내려간 경우

데이터 바인딩

- {{ }} : Mustache Tag(콧수염괄호), 가장 기본적인 데이터 바인딩 방식
- directive : 디렉티브는 뷰로 화면의 요소를 더 쉽게 조작하기 위한 문법 v- 로 시작한다.
- v-bind:id , v-bind:class 를 사용하여 Vue인스턴스가 관리하는 data(id, class) 와 서로 연결할 수 있다.

v-if 와 v-show의 차이점

- v-if는 false일 때 해당 DOM을 제거한다. v-show는 css속성인 display: 'none' 속성으로 육안상으로 안보이도록 한다.

Input 박스의 데이터 바인딩

- v-model을 사용하여 vue의 data와 동기화 시킬 수 있다.

v-on:keyup.enter를 사용하면 사용자의 키보드 입력을 바인ㄷ, 할수 있다.

watch 속성

- watch 속성은 기본적으로 데이터를 대상으로 넣을 수 있고 데이터의 변화에 따라서 특정 로직을 실행할 수 있는 속성이다.
- watch 속성으로 특정 값을 추적한다면 newValue, oldValue 두가지의 인자를 넣을 수 있다.

watch 와 computed

- 서로간의 공통점으로는 data의 값에 의존성을 가지고 있다.
- computed는 validation을 주로 사용함, watch는 주로 무거운 로직들 (매번 실행되기 어려운것들)
- computed는 주로 텍스트, 연산등의 간단한것들, watch는 데이터등의 무거운 것들(axios) 요청
- watch의 남용은 코드가 더러워 진다.


[VUE-CLI 3.x]

- 생성 : vue create '프로젝트 폴더 위치'
- 실행 : npm run serve
- <template> 내부에는 가장 먼저 html 태그가 있어야한다.
- props 내려주기
  <app-header v-bind:프롭스 속성 이름="상위 컴포넌트의 데이터 이름"></app-header>
- 기존에는 data에 값을 넣을 때 객체를 넣었는데 컴포넌트를 만들때는 export default 내부에서 data를 다른 컴포넌트간의 참조가 일어나지 않도록 데이터에 function을 연결하여 새 객체를 리턴하도록 한다.
- v-model : input과 data의 양방향 바인딩을 한다.
    
    
    ## Vue 완벽가이드 강의

#1일차.

 Vue Router
- router 사용 시 router폴더 생성 index.js 만들고 route 등록
- redirect 사용은 
    {
      path: "/",
      redirect: "/news",
    },

 이런식으로 redirect 패스를 지정해준다.
 
- routes 폴더에 있는 View.vue 파일들에는 axios라던지 같은 데이터를 다루기 보다는 라우팅 정보만 가지고 있는 것이 좋다. data를 다루는 ( 비즈니스로직) 것들은 따로 컴포넌트로 만드는 것이 좋다.
 api는 보통 api폴더를 생성하여 정리해놓는다.
 - axios등의 라이브러리 로딩을 각 페이지마다 정의해놓는것은 불필요 작업이다.
 - api 폴더 내부에 index.js 내부에는 axios.get() 의 프로미스를 리턴해주는 함수 정의
 - 정의한 함수들은 필요한 VIEW 파일 내부의 created, beforeMounted에서 사용한다. 
 - api를 사용하고 then 내부에서 this.data에 접근할 수 없는데 이 때 api 함수위에 var vm = this; 를 사용하여 data에 접근할 수 있다.
 
Javscript의 this
 -  this는 기본적으로 전역을 가리킨다.
 -  생성자 함수 내부에서의 this는 객체 자신을 가리킨다.
 -  비동기 처리에서의 this : 화살표 함수를 사용하여 바인딩을 그대로 가져간다. (컴포넌트를 가리킴)


콜백 
 - 어떤 특정 기능이 종료되자마자 실행되는 함수
 - 자바스크립트는 함수를 인자로 넣을 수 있다 
 
자바스크립트의 전역객체 (Global Obejct) 
 - 자바스크립트는 최상위에 1개의 전역객체를 가진다. 
 - 자바스크립트는 소스가 실행하기 전에 , 최상위에 위치한 전역객체를 만든다.( Math나 Data를 비롯한 몇몇 특별한 객체 제외) 자바스크립트의모든 객체와 값들은 이 전역 객체의 아래에 자손으로 위치하게 된다. 전역객체는 전체 코드에서 단 1개만 존재할 수 있으며, new 연산자를 이용하는 방법들으로 새롭게 만들 수 없다. 
 - 이 전역객체의 이름은 자바스크립트를 사용하는 환경에 따라 얼마든지 달라질 수 있다. 이를테면 웹 브라우저에서 사용되는 자바스크립트의 전역객체는 우리가 잘 아는 window라는 이름의 객체이다. 
 - 자바스크립트에서는 코딩할 때 전역객체를 생략할 수 있다.
 
객체 
 - 객체를 완성하는 구성요소들은 프로퍼티와 메소드이다.
 - 프로퍼티 : 객체의 속성을 나타내는 접근 가능한 이름과 활용 가능한 값을 가지는 특별한 형태
 - 메소드 : 객체가 가지고 있는 동작 , 메소드를 수행하기 위해서는 객체를 통해서 해당 메소드를 수행하여야 한다. 즉 이 동작을 수행하는 주체는 객체이며, 이 동작을 수행하기 위해서는 객체에게 동작을 수행하라고 지시해야 한다. 반대로 함수는 스스로가 실행될 수 있는것이다.
  
자바스크립트이 객체(Object) 구성
 - Built-in Object( 자바스크립트 내장객체) : Global, Obejct, String, Number, Boolean, Date, Array, Math, RegExp, Error 등 많은 내장객체들이 있다.
   이들은 자바스크립트 엔진이 구동되는 시점에서 바로 제공되며, 자바스크립트 코드 어디에서는 사용이 가능하다.
- Native Object( 브라우져 내장 객체 ) : 자바스크립트가 구동되는 시점에서 바로 사용한 객체들이다. 하지만 이들은 자바스크립트 엔진이 구성하는 기본객체라고 하기 보단 브라우져 즉 자바스크립트 엔진을 구동하는 녀석들에게서 빌드되는 객체들이다. 자바스크립트 프로그램을 작성하면서 사용하는 브라우져 객체모델(BOM) 과 문서객체모델(DOM) 이 이에 속한다. 이 객체들은 Built-in Object 가 구성된 후에 구성된다. 이 Native Object 역시 내장객체이다. Native Object라 분류한 이유는 브라우져마다 이 Native Object를 사용함에 있어서 그 구성을 달리하는 경우가 있기 때문이다.

- Host Object( 사용자 정의 객체 ) :  말그대로 사용자가 생성한 객체들이다. constructor 혹은 객체 리터럴을 통해 사용자가 객체를 정의하고 확장시킨 녀석들이기 때문에 Built-in Object와 Native Object가 구성된 이후에 구성되어진다. constructor를 사용하여 객체생성 할 경우 new 키워드를 사용해 다중 객체를 생성할 수 있으나 JSON을 이용하여 만들면( var foo = {} ) 단일 객체로만 활용된다.
 
Obejct 객체 
 - 자바스크립트에서 생성되는 객체는 Object 객체에서 파생되어 나온 객체들이라는 것과 이들은 암묵적으로 Array 객체를 상속한다.
 - Object 객체는 Built-in 객체로서 최상위레벨의 객체이다. 즉 모든 객체는 이 Object 객체에서 파생되어 나온 확장형태 인 것이다.  Object객체라는 최상위 객체를 껍대기로 파생되는 객체들은 Object 객체가 가지고 있는 기본적인 구성요소를 상속받게 된다. 사실 자바스크립트의 모든 객체가 자유롭게 확장 될 수 있는것도 Object객체가 가진 특별한 구성요소 때문이다. Object객체가 가진 특별한 구성요소들은 constructor, prototype, 이라는 프로퍼티와 hasOwnProperty() , toString(), isPrototypeOf() 라는 메소드들이다. 자바스크립트의 모든 객체가 Obejct에서 파생 되었다는 것은 객체를 생성할 때 사용된 생성자 함수의 prototype을 저장하는 _proto_ 를 통해 알 수 있으며 객체들이 기본적으로 가지는 메소드들을 보면서 확인 할 수 있다. 

Obejct(객체) 의 배열상속
 - 자바스크립트의 객체는 곧 배열이다. 이를 증명할 방법은 많다. 가장 간단한 방법은 객체의 메소드는 객체 안에 존재하지 않는다. 메소드를 소유한 parent객체는 객체에 포함된 메소드들의 참조값만을 가지고 있다. 즉 메소드들 자체도 각각 개별 객체로서 존재한다.  즉 객체는 자기 자신을 이루는 요소들을 저장한 배열들의 집한체이며 이들은 chain 이라는 연결 구조를 가지고 있다.

Obejct prototype에 대한  이해
 -  프로토타입 기반 프로그래밍 : 객체의 원형인 프로토타입을 이용하여 새로운 객체를 만들어내는 기법이다. 이렇게 만들어진 객체 역시 자기자신의 프로토타입을 갖는다. 이 새로운 객체의 원형을 이용하면 또 다른 새로운 객체를 만들어 낼 수도 있으며 이런 구조로 객체를 확장하는 방식을 프로토 타입 기반 프로그래밍이라고 한다. 
 - 자바스크립트에서 사용되는 프로토타입이란 용어는 크게 두가지로 나눈다. Prototype Property가 가리키고 있는 Prototype Obejct 와 자기 자신을 만들어낸 객체의 원형을 의미하는 Prototype Link이다. 자바스크립트 관련 레퍼런스는 대부분 프로토타입에 대한 정의는 객체의 원형을 의미하는 Prototype Link로 정의하지만 Prototype Property 를 이용한 객체 확장에 대해서만 다루기 때문에 이 둘의 차이를 자세히 거론 하지 않는다. 그런 이유로 자바스크립트의 프로토타입을 공부하는 사람들은 Prototype Property가 자바스크립트에서 말하는 프로토타입이라고 이해하고 이를 사용한다. 

자바스크립트의 프로토타입( Prototype ) 이란? 
 - 자바스크립트의 모든 객체는 자신을 생성한 객체 원형에 대한 숨겨진 연결을 갖는다.  이때 자기 자신을 생성하기 위해 사용된 객체원형을 프로토타입이라고 한다. 자바스크립트의 모든 객체는 Obejct 객체의 프로토타입을 기반으로 확장 되었기 때문에 이 연결을 끝은 Object 객체의 프로토타입 Object이다. 즉 어떠한 객체가 만들어지기 위해 그 객체의 모태가 되는 녀석을 프로토타입이라고 한다. 

 - function A() {} , var A = new A() console.log(A) 를 하면  나오는것중 __proto__ 와 constructor를 주의깊게 봐야한다. __proto__ 바로 이녀석이 A라는 객체를 만들어내기 위해 사용된 객체원형에 대한 숨겨진 연결이다.  해당객체의 프로토타입은 A라는 함수객체이며 이 객체의 생성자 역시 funtion A() 함수라는 것이다.  즉 new Operator를 통해 만들어진 객체는 function A() 를 자신의 프로토타입으로 사용하여 만들어졌다는 말이다. 보통 기초가 부족한 사람들에게의 프로토타입이란 자신을 만들어낸 객체원형을 의미하는것이 아니고, 애석하게도 prototype프로퍼티이다.

자바스크립트의 프로토타입(Prototype) 프로퍼티 란?
 - 모든 함수 객체의 Constructor는 prototype이란 프로퍼티를 가지고 있다.  이 prototype 프로퍼티는 객체가 생성될 당시 만들어지는 객체 자신의 원형이 될 prototype객체를 가리킨다. 즉 자신을 만든 원형이 아닌 자신을 통해 만들어지는 객체 자신의 원형이 될 prototype 객체를 가리킨다. 
prototype object 는 default로 empty Object를 가리킨다. 
- 참고 : 프로토타입은 자기 자신을 생성하게 한 자신의 원형 객체라고 정의했다. 그럼 그 원형객체란 프로토타입은 function A() 함수일까? 절대 아니다.
   자바스크립트의 모든 객체는 생성과 동시에 자기자신이 생성될 당시의 정보를 취한 Prototype Object 라는 새로운 객체를 Cloning하여 만들어낸다. 프로토 타입이 객체를 만들어내기 위한 원형이라면 이 Prototype Object 는 자기 자신의 분신이며 자신을 원형으로 만들어질 다른 객체가 참조할 프로토타입이 된다. 즉 객체 자신을 이용할 다른 객체들이 프로토타입으로 사용할 객체가 Prototype Object 인 것이다. 즉 위에서 언급한 __proto_ 라는 prototype 에 대한 link는 상위에서 물려받은 객체의 프로토타입에 대한 정보이며 prototype 프로퍼티는 자신을 원형으로 만들어질 새로운 객체들 즉 하위로 물려줄 연결에 대한 속성이다.
 
- 모든 객체의 확장은 객체가 소유한 prototype Object를 통해 이루어지며 이 연결의 끝은 이전 글에서 소개한 Object객체의 prototype Object가 된다. 일반적으로 자바스크립트의 코드를 통해 다루는 prototype이 객체가 소유한 자기자신의 prototype Object 이기 때문에 대부분의 자바스크립트 입문자는 프로토타입이란 것을 prototype property라고 생각하게되는 오류를 범하는 것이다. 


- 예제)
   function foo(x) {
        this.x = x;
    } 
    var A = new foo('hello');
    console.log( A.x );
 > hello

   console.log(A.prototype.x)
> syntax error 

 prototype 프로퍼티는 Constructor 가 가지는 프로퍼티 이다. 그리고 함수객체만 이 프로퍼티를 가지고 있다고 했다. A객체는 함수객체가 아니다. foo 라는 원형을 이용하여 함수객체를 통해 만들어진 Object 객체에 확장된 단일 객체일 뿐이다. 즉 A는 prototype 프로퍼티를 소유하고 있지 않기에 A.prototype.x가 syntax error 가 된다. 즉 프로토타입을 이해하려면 foo.prototype.x 는 OK , A.prototype.x 는 ERROR 를 반드시 이해 하고 기억하자.


-  Prototype Obejct 는 A가 생성될 당시의 정보만을 가지기 때문에  이후 정보는 모른다. 


자바스크립트의 프로토타입 체인 ( Prototype Chain) 
 - 객체의 생성과정에서 모태가 되는 프로토타입과 연결고리가 이어져 상속관계를 통하여 상위 프로토 타입으로 연속해서 이어지는 관계를 프로토타입 체인이라고 한다. 이 연결은 __proto__ 를 따라 올라가게 된다. 
  - 즉 , 프로토타입 체인이란 프로토타입을 상속해서 만들어지는 객체들관의 연관관계를 의미한다.  그림에서 __proto__ 프로퍼티들간 이어진 점선을 타고 가다보면 최종적으로 Object객체의 prototype Object에 다다른다.  이러한 프로토타입 체인은 하위객체에서 상위객체의 프로퍼티와 메소드를 상속받는다. 그리고 동일한 이름의 프로퍼티와 메소드를 재정의 하지 않는 이상 상위에서 정의한 내용을 그대로 물려받는다.( 공유 ) 

 - Prototype Object 의 x 메소드를 재정의 하였을 때 B, C 객체에도 그 영향을 받는다. 그리유는 프로토타입의 체인에 의한 공유 때문이다. 
 - 
    var A = function () { };
A.prototype.x = function () {
     console.log('hello');
};
var B = new A();
var C = new A();

B.x();
> hello 

C.x();
> hello 

A.prototype.x = function () {
     console.log('world');
};

B.x();
> world

C.x();
> world
 여기서 유심히 봐야할것은 A Prototype Object가 소유한 Constuctor이다. A Prototype Object의 Constuctor는 A객체의 생성자 함수이다. 즉 이를 통해 만들어지는 객체들은 A객체가 생성될 당시 소유하고 있지 않은 x 라는 메소드를 가질 수 없다.  x 는 A.prototype을 이용하여 A Prototype Object에 추가 되어진 메소드다. 하지만 이 x 메소드는 프로토타입 체인에 의한 공유 메소드이다. A 의 Prototype Object가 소유한 x 라는 메소드는 A Prototype Object 를 프로토타입으로 만들어진 모든 객체에서 사용할 수 있다. 이는 프로토타입 기반 송속에서 매우 중요한 특성을 말한다. 
 위 예제에서 사용한 x라는 메소드를 하위객체에서 찾지 못하면 상위객체에서 해당 메소드를 탐색한다. 이런 방법으로 프로토 타입 체인을 따라 최상위 객체까지 도달할 때까지 해당메소드를 찾지 못한다면 undefined가 되는 것이다. 

- 하지만 A 객체가 생성당시 x 라는 메소드 혹은 의미있는 프로퍼티에 대한 정의가 포함된 내용을 가지고 있다면 이들은 공유가 아닌 상속된다.


 이벤트 버블링
 - 이벤트 버블링은 특정 화면 요소에서 이벤트가 발생했을 때 해당 이벤트가 더 상위의 화면 요소들로 전달되어 가는 특성이다.
 - 브라우저는 특정 화면 요소에서 이벤트가 발생했을 때 그 이벤트를 최상위에 있는 화면 요소까지 이벤트를 전파 시킨다. 

이벤트 캡쳐 
 - addEventListener() API 에서 옵션 객체에 capture: true 값을 설정해준다. 그러면 해당 이벤트를 감지하기 위해 이벤트 버블링과 반대방향으로 탐색한다.

event.stopPropagation()
 - 해당 이벤트가 전파되는것을 막는다. 이벤트 버블링의 경우에는 클릭한 요소의 이벤트만 발생시키고 상위요소로 이벤트를 전달하는 것을 방해한다. 그리고 이벤트 캡쳐의 경우에는 클릭한 요소의 최상위 요소의 이벤트만 동작시키고 하위요소들로 이벤트를 전달하지 않는다.

이벤트 위임 - Event Delegation
 - 이벤트위임은 하위 요소에 각각 이벤트를 붙이지 않고 상위요소에서 하위 요소의 이벤트들을 제어하는 방식이다.
 ex) 기존에 querySelectorAll을 사용하여 li 태그를 가져오고 addEventListener를 사용, 이벤트를 등록한 2개의 li태그가 있다고 하고 
input.setAttribute('type', 'checkbox');
input.setAttribute('id', 'item3');
label.setAttribute('for', 'item3');
와 같은 코드를 사용해서 새로 추가하게 될 때 해당 li태그는 이벤트를 가지고 있지 않다. 위와 같이 매번 새로운것이 추가 될 때 이벤트리스너에 등록되지 않은 태그를 등록하고자 할 떄 필요한것이 이벤트 위임이다. 예를 들어 기존에는 li태그들을 가져와서 리스너를 부여했다면 li의 상위의 ul에 리스너를 넣으면 이벤트 버블링으로 인해 모든 li태그들은 해당 이벤트를 가지게 된다.
 


