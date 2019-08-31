Inflearn Vue 1일차

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

$$
$$
