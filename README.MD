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

