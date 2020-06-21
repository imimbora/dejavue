# dejavue
why is vue always new


공부한 내용 정리

2020.06.16

\- vetur 패키지 설치

\- ! + tab : html 보일러 플레이트를 만들어줌

div 태그에 #app 를 부여한 후
script 단에 뷰에서 제공하는 함수 `new Vue` 를 이용해서 <b>뷰 인스턴스 생성</b><br>
함수 안에 object {} 를 만들고 `el:` 에 `#app`

`this.person.name` 이 가능한 것은
`data` 에 있는 내용을 `this` 안에 넣어주기 때문 <br>
`methods` 아이들도 앞에 this. 를 붙여 다른 메소드 안에서 사용가능

함수를 사용할 때 인자 argument 를 넣어주고 <br>
함수 안에서 설정될 매개변수 parameter 로 받아 사용할 수 있다.

대부분의 html태그 속성 앞에 : 을 붙여 <b>데이터 바인딩</b> <br>
`(v-bind):`

<b>이벤트</b> <br>
onclick 속성 => `v-on:click`

`<form>` 은 submit 시 페이지를 리로드

자바스크립트에서는 preventDefault 로 기본기능을 막는 대신 <br>
뷰에서는 이벤트 핸들링 > 이벤트 수식어 중
클릭 이벤트 전파를 중단하는 `.prevent` 가 있다.

`<form v-on:submit.prevent="submit">`

<b>데이터 양방향 바인딩</b> (v-model) <br>
input 입력시 미리보기

`v-on:keyup` 이벤트 <br>
`v-on:` 은 @ 로 대체 <br>
함수에 따로 인자를 넣어주지 않았지만 <br>
keyup 이벤트에서 자동으로 키보드 이벤트가 발생할 때마다 object 를 인자로 받아옴
(01.html)

\+ 비고 <br>
임임 뒤에 '은/는' 중에 붙이도록 응용<br>
( 한글에 조사를 붙여주는 josa.js 참조 )


2020.06.21

`:value="text" @keyup="updateText"` 대신 `v-model="text"` 로 바꾸고<br>
updateText 함수도 필요없어짐 (02.html)

computed
복잡한 계산식을 치환하면서 중복제거의 효과

*methods 와 비교<br>
함수를 사용할 때는 () 괄호를 붙여줘야하고<br>
computed 속성은 데이터 변수를 쓰는 것처럼 괄호 없이

같은 결과값<br>
https://kr.vuejs.org/v2/guide/computed.html#computed-속성의-캐싱-vs-메소드

여러 군데일 때
computed 는 처음 1번만 계산이 되어 저장(캐싱)되어 있는 값을 세 군데에서 쓴다면<br>
methods 는 만날 때마다 계산 ! 3번 함수를 반복해서 사용
