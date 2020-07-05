# 뷰js 2 (vuejs 2) 기초 익히기 기본 강좌

01~04 : index.html

- 임임 뒤에 '은/는' 중에 붙이도록 응용 ( 한글에 조사를 붙여주는 josa.js 참조 )

## 01 뷰 인스턴스 생성하기

vetur : vs code의 vue관련 확장프로그램
! + tab : html 보일러 플레이트를 만들어줌

div 태그에 #app 를 부여한 후 script 단에 뷰에서 제공하는 함수 `new Vue` 를 이용해서 **뷰 인스턴스 생성**  
함수 안에 object {} 를 만들고 `el:` 에 `#app`

## 02 뷰 데이터 (data) 와 메소드 (methods)

`this.person.name` 이 가능한 것은 `data` 에 있는 내용을 `this` 안에 넣어주기 때문  
`methods` 아이들도 앞에 this. 를 붙여 다른 메소드 안에서 사용가능

함수를 사용할 때 인자 argument 를 넣어주고  
함수 안에서 설정될 매개변수 parameter 로 받아 사용할 수 있다.

## 03 데이터 바인딩 (Data Binding)

대부분의 html태그 속성 앞에 : 을 붙여 **데이터 바인딩** `(v-bind):`

## 04 이벤트 (Events)

**이벤트**  
onclick 속성 => `v-on:click`

`<form>` 은 기본적으로 submit 시 페이지를 reload

자바스크립트에서 기본기능을 막는 preventDefault 대신
뷰에서는 이벤트 핸들링 > 이벤트 수식어 중 클릭 이벤트 전파를 중단하는 `.prevent` 가 있다.

`<form v-on:submit.prevent="submit">`

[이벤트 핸들링 | Vue.js](https://kr.vuejs.org/v2/guide/events.html)

## 05 데이터 양방향 바인딩 (Data Two Way Binding - v-model)

`v-on:keyup` 이벤트  
`v-on:` 은 '@' 로 대체  
함수에 따로 인자를 넣어주지 않았지만  
keyup 이벤트에서 자동으로 키보드 이벤트가 발생할 때마다 object 를 인자로 받아옴 (01.html)

```html
<form v-on:submit.prevent="submit">
  <input type="text" :value="text" @keyup="updateText" />
  {{ text }}
  <button type="submit">Submit</button>
</form>
```

```js
new Vue({
  el: "#app",
  data: {
    text: "text",
  },
  methods: {
    submit() {
      console.log("submitted");
    },
    updateText(event) {
      this.text = event.target.value;
    },
  },
});
```

`:value="text" @keyup="updateText"` 대신 `v-model="text"` 로 바꾸고  
updateText 함수도 필요없어짐 (02.html)

```html
<form v-on:submit.prevent="submit">
  <input type="text" v-model="text" />
  {{ text }}
  <button type="submit">Submit</button>
</form>
```

## 06 Computed 속성

computed 복잡한 계산식을 치환하면서 중복제거의 효과

\*methods 와 비교  
함수를 사용할 때는 () 괄호를 붙여줘야하고  
computed 속성은 데이터 변수를 쓰는 것처럼 괄호 없이

같은 결과값
[computed-속성의-캐싱-vs-메소드 | Vue.js](https://kr.vuejs.org/v2/guide/computed.html#computed-속성의-캐싱-vs-메소드)

vue 인스턴스가 생성될 때 data 내 `message: '헬로우'` 를 가지고있고 computed 속성이 바로 발휘되면서
`reversedMessage` 라는 computed 속성이 생김
`{{ reversedMessage }}` 에 접근할 때는 이미 계산이 되어있음

여러 군데일 때 computed 는 처음 1번만 계산이 되어 저장(캐싱)되어 있는 값을 세 군데에서 쓴다면  
methods 는 만날(호출할) 때마다 계산 ! 3번 함수를 반복해서 사용
message 값이 변경된다면 변경된 값을 캐치해서 다시 계산해 다시 세군데에 적용
= data 값이 바뀌지 않는한 처음에 계산된 값을 계속 가지고있다.
