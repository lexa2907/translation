<template>
  <div class="flex-container">
     <main>
       <section class="flex-item item-3">
         <img src="mmm2.jpg" />
         <div class="caption">
             <p class="p1">UFC 302: МАХАЧЕВ VS ПОРЬЕ</p>
             <p class="p2">ВОСКРЕСЕНЬЕ, 2 ИЮНЯ 2024 Г., 1:15</p>
             <!-- <p style="font-size: 1rem; ">Начало ранних прелимов - в 01:00, прелимов - в 03:00, главного карда - в 05:00 по Москве. </p> -->
             <a href="#part1" class="atuin-btn">Смотреть</a>
         </div>
       </section>
       <section class="flex-item item-4">
         <div><a href="https://1wyvou.top/?open=register" target="_blank"><img src="kkk.jpg" /></a></div>
         <div><a href="https://1wyvou.top/?open=register" target="_blank"><img src="llm.jpg" /></a></div>
        <div><a href="https://1wyvou.top/?open=register" target="_blank"><img src="lll.jpg" /></a></div>
       </section>
       <section class="flex-item item-5">
      <div class="add-height">
      <div id="part1" class="textTranslation">ПРЯМАЯ ТРАНСЛЯЦИЯ</div>
      <div class="btn-group">
        <button v-on:click="greet('chart1')" style="width:33.3%" :class="{activeChartClass: activeChart === 'chart1'}">Трансляция №1</button>
        <button v-on:click="greet('chart2')" style="width:33.3%" :class="{activeChartClass: activeChart === 'chart2'}">Трансляция №2</button>
        <button v-on:click="greet('chart3')" style="width:33.3%" :class="{activeChartClass: activeChart === 'chart3'}">Трансляция №3</button>
      </div>
      <iframe v-if="activeChart === 'chart2'" class="iframeClass" src="https://vk.com/video_ext.php?oid=-223069695&id=456239021&hash=9ed0fd1a3643d920" width="1000px" height="640px" frameborder="0" allowfullscreen="true" scrolling="no" sandbox="allow-same-origin allow-scripts" allow="encrypted-media; fullscreen; picture-in-picture;"></iframe>
      <iframe v-if="activeChart === 'chart1'" class="iframeClass" src="https://live.vkplay.ru/app/embed/mix111" frameborder="0" allowfullscreen="true" scrolling="no" sandbox="allow-same-origin allow-scripts" allow="encrypted-media; fullscreen; picture-in-picture;"  width="1000px" height="640px"></iframe>
      <iframe v-if="activeChart === 'chart3'" class="iframeClass" src="https://live.vkplay.ru/app/embed/mix111" frameborder="0" allowfullscreen="true" scrolling="no" sandbox="allow-same-origin allow-scripts" allow="encrypted-media; fullscreen; picture-in-picture;"  width="1000px" height="640px"></iframe>
      <video-player crossorigin="anonymous" v-if="activeChart === 'chart4'"  class="playerTranslation" @get-instance="getInstance" :option="option" :key="option.url" />
     </div>
       </section>
     </main>
   </div>
   <popup-sub
       :is-open="isPopupOpen"
       @ok="popupConfirmed"
     >
       <p style="margin-bottom: 1em; margin-top: 1em;">Для бесплатного просмотра трансляции нужно только подписаться на telegram канал</p>
       <hr />
     <p style="font-size:0.9rem; margin-bottom: 3em;  margin-top: 1em;">После подписки на канал в течение 5 секунд данное окно пропадет и вы сможете смотреть трансляцию</p>
     </popup-sub>

   
 </template>
 
 <script>
 import VideoPlayer from "./MyPlayer.vue";
 import PopupSub from './PopupSub.vue';
 import {useCookies} from 'vue3-cookies'

 const {cookies} = useCookies();
 
 export default {
   data() {
     return {
       componentKey: "https://e5.varcdn.top/matchboec/tracks-v1a1/mono.m3u8",
       option: {
         container: ".artplayer-app",
         url: "https://e5.varcdn.top/matchboec/tracks-v1a1/mono.m3u8",
         autoMini: true,
       },

       activeChart : 'chart1',
      //  isPopupOpen: !cookies.get("authorized"),
       isPopupOpen: false,
     };
   },
   components: {
     VideoPlayer,
     PopupSub,
   },

   methods: {
     getInstance(art) {
       console.log(art);
     },
     greet: function (text) {
     if (text === 'chart1') {this.option.url = ""} 
     else if (text === 'chart2') {this.option.url = ""}
     else if (text === 'chart3') {this.option.url = ""}
     this.activeChart = text;
   },

   popupConfirmed() {
     window.open('https://www.google.com', "_blank")
     cookies.set("authorized", true, "7d")
     setTimeout(function(){
       this.isPopupOpen = false;
 }.bind(this),5000);
   },
   },
 };
 </script>
 
 <style>
 .add-height {
   width: 1000px;
   height: 800px;
   margin: 100px auto 0;
   text-align: center;
 }
 .btn-group button {
   border: 1px solid green; /* Green border */
   background-color: #202120;
   color: white; /* White text */
   padding: 10px 24px; /* Some padding */
   cursor: pointer; /* Pointer/hand icon */
   float: left; /* Float the buttons side by side */
 }
 /* Clear floats (clearfix hack) */
 .btn-group:after {
   content: "";
   clear: both;
   display: table;
 }
 .btn-group button:not(:last-child) {
   border-right: none; /* Prevent double borders */
 }
 /* Add a background color on hover */
 button:hover {
   background-color: #a5a6a8;
 }
 .activeChartClass {
   background-color:  #a5a6a8!important;
}
.textTranslation{
 font-size: 3rem;
 margin-bottom: 0.5em;
}
.playerTranslation{
 width: 100%;
 height: 80%;
}
.caption {
   position: absolute;
   top: 70%;
   left: 50%;
   transform: translate( -50%, -50% );
   text-align: center;
   color: white;
   font-weight: bold;
}
.p1{
  font-size: 2.5rem;
   margin-bottom: 0.2em;
}
.p2{
  font-size: 1.7rem;
   margin-bottom: 0.6em;
}
.atuin-btn {
   display: inline-flex;
   margin: 10px;
   text-decoration: none;
   position: relative;
   font-size: 30px;
   line-height: 30px;
   padding: 12px 30px;
   color: #FFF;
   font-weight: bold;
   text-transform: uppercase; 
   font-family: 'Roboto', Тahoma, sans-serif;
   background: rgba(28,28,28,0);
   cursor: pointer; 
   border: 2px solid #BFE2FF;
   overflow: hidden;
   z-index: 1;
}
.atuin-btn:hover,
.atuin-btn:active,
.atuin-btn:focus {
   color: #FFF;
}
.atuin-btn:before {
   content: '';
   position: absolute;
   top: 0;
   right: -50px;
   bottom: 0;
   left: 0;
   border-right: 50px solid transparent;
   border-top: 50px solid #272828;
   transition: transform 0.5s;
   transform: translateX(-100%);
   z-index: -1;
}
.atuin-btn:hover:before,
.atuin-btn:active:before,
.atuin-btn:focus:before {
   transform: translateX(0);
}
.item-4 {
 background: linear-gradient(45deg, #070707, #3d3c3c);
 flex: 2;
 min-height: 50vh;
 display: flex;
}
.item-3 {
 background: linear-gradient(45deg, #070707, #3d3c3c);
 flex:3;
 min-height: 100vh;
}
img
 {
 width: 100%;
 height: 100%;
 }
 .item-5 {
 background: linear-gradient(45deg, #070707, #3d3c3c);
 flex: 2;
 min-height: 70vh;
 display: flex;
}




@media (max-height: 500px) and (min-width: 500px) and (max-width: 1000px){
 .add-height{
 height: 380px;
 width: 700px;
 margin: 0 auto;
 }
 .iframeClass{
 height: 380px;
 width: 700px;
 margin: 0 auto;
 }
 .textTranslation{
   font-size: 1.4rem;
   margin-bottom: 0em;
 }
 .btn-group button {
   padding: 5px 24px; /* Some padding */
 }
 .item-5 {
 background: linear-gradient(45deg, #070707, #3d3c3c);
 flex: 2;
 min-height: 100vh;
 display: flex;
}
}

@media (max-width: 501px){
 .add-height {
   width: 350px;
   height: 300px;
   /* margin: 0 auto; */
 }
 .iframeClass {
   width: 350px;
   height: 300px;
   /* margin: 0 auto; */
 }
 .textTranslation{
 font-size: 1.5rem;
 margin-bottom: 0.5em;
 
}
.btn-group button{
 font-size: 0.5rem;
 padding: 4px 24px; /* Some padding */
}
.caption {
   position: absolute;
   top: 37%;
   left: 50%;
   transform: translate( -50%, -50% );
   text-align: center;
   color: white;
   font-weight: bold;
}
.p1{
  font-size: 1.5rem;
   margin-bottom: 0.2em;
}
.p2{
  font-size: 0.6rem;
   margin-bottom: 0.6em;
}
.atuin-btn {
  margin: 0px;
   position: relative;
   font-size: 15px;
   line-height: 5px;
}
.item-4 {
 min-height: 0vh;
}
.item-3 {
  background-size: cover;
 /* min-height: 0vh; */
}
}



* {
 margin: 0;
 padding: 0;
 box-sizing: border-box;
}

.flex-item {
 padding: 10px;
 font: 900 60px "Roboto", sans-serif;
 color: #fff;
 text-align: center;
 text-shadow: 4px 2px 0 rgba(0, 0, 0, 0.2);
}

.item-4 div {
 background: #fff;
 width: 33%;
 margin: 4px;
 
 color: #000;
 font-size: 16px;
}


/* Custom styles */
.flex-container {
 display: flex;
 flex-direction: column;
}

main{
 display: flex;
 flex-direction: column;
 
}
</style>
