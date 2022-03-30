<!-- 메인페이지 -->
<template>
  <div class = "black-bg" v-if= " view == ture ">
    <div class = "white-bg">
      <h4>상세페이지임</h4>
      <span>상세내용임</span> <button @click="view = false"> 닫기 </button> 
    </div>
  </div>
  
  <!-- 이곳에 HTML 코드 관리 -->
  <div class = menu>
    <!-- vue html 반복문 문법 사용 -->
    <!-- value: menu의 각 원소를 가져옴 , index: 0부터 1씩 증가하는 정수  :key=횟수 가 들어가는것이 일반적임 -->
    <a v-for ="(value,index) in menu" :key="index" > {{value}} </a> 
  </div>

  <div class = objcard>
    <div v-for = "(dbdata, index) in dbdata" :key="index">     
      <img class = image :src= "dbdata.image"/>
      <h4 class = productName :style = "atr" @click="view = ture"> {{ dbdata.title }}  </h4>
      <!-- 속성 데이터 바인딩은 속성 앞에 :(콜론을 붙인다.) -->    
      <p>{{ dbdata.price / 10000 }} 만원</p>
      <p>{{ dbdata.content }}</p>
      <!-- {{ 오브젝트 키 }} 형식으로 데이터 주입-->
      <button @click ="increase(index)"> 허위매물신고 </button> <span> 신고수 : {{num[index]}} </span>
      <!--@click vue 문법임 -->
    </div>
  </div>
 
</template> 

<script>
  //이곳에 JS 코드관리

import roomdata from './rooms.js'; // js 데이터를 불러와서 사용할때 

export default { 
  data(){ //데이터 바인딩 데이터를 사용할때 오브젝트 형식 {} 으로 저장
    return{
      dbdata : roomdata, // 데이터 바인딩을 사용하여 데이터를 주입 할 수 있음
      view : false,
      num : [0,0,0,0],
      atr : 'color : blue', // 속성 또한 바인딩 가능
      menu : ['home', 'info', 'about'],
      name : ['태전동원룸', '곤지암원룸','송정동원룸'],
      // App.vue 의 경로가 src안에 있는데 왜 ./assets/room0.jpg 는 안되는건지....
      picture : ["../src/assets/room0.jpg", '../src/assets/room1.jpg','../src/assets/room2.jpg'],
      price: [60, 90, 40] 
    }
  },
  // 이곳이 함수(메소드)를 만들고 관리하는 공간.
  methods : {
    increase(index){
      this.num[index]++;
    }
  },
}  

</script>

<style>
/* 이곳에 CSS 관리 */
/* 모달창 기본 UI */
body {
  margin : 0;
}
div {
    box-sizing: border-box;
}
.black-bg {
  text-align: center;
  width: 100%; height: 100%;
  background: rgba(0,0,0,0.5);
  position: fixed; padding: 20px;
}
.white-bg {
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;
}
/* 위 까지 모달창 기본 UI */
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
.objcard {
  margin-top: 10px;
}

.menu {
  text-align: center;
  color : black;
  padding : 25px;
  background : #fbceb1;
  border-radius : 5px;
  
}

.menu a {
  padding : 20px;
}

.image {
  width : 100%;
}  


</style>

