<template>
  <div class="header">
    <ul class="header-button-left">
      <li>Cancel</li>
    </ul>
    <ul class="header-button-right">
      <li v-if="step == 1"  @click="step++">Next</li>
      <li v-if="step == 2" @click="publish">발행</li>
    </ul>
    <img src="./assets/logo.png" class="logo" />
  </div>

  <Container @write="작성한글 = $event" :이미지 = "이미지" :게시물="게시물" :step="step"/>
  <button @click="more">더보기</button>

  <div class="footer">
    <ul class="footer-button-plus">
      <input @change="upload" type="file" id="file" class="inputfile" />
      <label for="file" class="input-plus">+</label>
    </ul>
  </div>
  
  <!-- <div v-if="step == 0">내용0</div>
  <div v-if="step == 1">내용1</div>
  <div v-if="step == 2">내용2</div>
  <button @click="step = 0">버튼0</button>
  <button @click="step = 1">버튼1</button>
  <button @click="step = 2"> 버튼2</button>
  <div style="margin-top : 100px"></div> -->
  
</template>

<script>
import Container from './components/Container'
import postdata from './assets/postdata.js'
import axios from 'axios'


export default{
  name: "App",
  data(){
    return{
      step : 0,
      게시물 : postdata,
      이미지 : '',
      작성한글 : '',
    }
  },
  components:{
    Container,
  },
  methods: {
    more(){

      // axios.post('url',{name : 'kim'}).then().catch((err)=>{
      //   err
      // })

      axios.get(`https://codingapple1.github.io/vue/more${this.더보기}.json`)
      .then( 결과 => {
        this.게시물.push(결과.data);
      })
    },
    upload(e){
      let f = e.target.files;
      console.log(f[0].type);
      let url = URL.createObjectURL(f[0]);
      console.log(url);
      this.이미지 = url;
      this.step++;
    },
      publish(){
      var 내게시물 = {
        name: "Kim Hyun",
        userImage: "https://placeimg.com/100/100/arch",
        postImage: this.이미지,
        likes: 36,
        date: "May 15",
        liked: false,
        content: this.작성한글,
        filter: "perpetua"
    };
      this.게시물.unshift(내게시물);
      this.step = 0;
    },
  },
}
</script>

<style>
@import 'style.css';

</style>
