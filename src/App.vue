<template>
    <div class="add-height">
      <div class="textTranslation">ПРЯМАЯ ТРАНСЛЯЦИЯ</div>
      <div class="btn-group">
        <button v-on:click="greet('chart1')" style="width:33.3%" :class="{activeChartClass: activeChart === 'chart1'}">Трансляция №1</button>
        <button v-on:click="greet('chart2')" style="width:33.3%" :class="{activeChartClass: activeChart === 'chart2'}">Трансляция №2</button>
        <button v-on:click="greet('chart3')" style="width:33.3%" :class="{activeChartClass: activeChart === 'chart3'}">Трансляция №3</button>
      </div>
      <iframe v-if="activeChart === 'chart2'" class="iframeClass" src="https://p2pvar.top/stream/live/boyets.html" frameborder="0" allowfullscreen="true" scrolling="no" sandbox="allow-same-origin allow-scripts" allow="encrypted-media; fullscreen; picture-in-picture;"  width="1000px" height="640px"></iframe>
      <video-player v-if="activeChart !== 'chart2'" class="playerTranslation" @get-instance="getInstance" :option="option" :key="option.url" />
      <popup-sub
        :is-open="isPopupOpen"
        @ok="popupConfirmed"
      >
        Для бесплатного просмотра трансляции нужно только подписаться на telegram канал
        <hr />
      <p style="font-size:0.9rem">После подписки на канал в течение 5 секунд данное окно пропадет и вы сможете смотреть трансляцию</p>
      </popup-sub>
      </div>
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
        isPopupOpen: !cookies.get("authorized"),
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
      if (text === 'chart1') {this.option.url = "https://e5.varcdn.top/matchboec/tracks-v1a1/mono.m3u8"} 
      else if (text === 'chart2') {this.option.url = "https://varline.store/api/match?stream=https://p2pvar.top/stream/live/boyets.html"}
      else if (text === 'chart3') {this.option.url = "https://strm.yandex.ru/kal/udar/udar0.m3u8"}
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
    background-color: #4CAF50;
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
    background-color: #3e8e41;
  }
  .activeChartClass {
    background-color: #3e8e41!important;
}
.textTranslation{
  font-size: 3rem;
  margin-bottom: 0.5em;
}
.playerTranslation{
  width: 100%;
  height: 80%;
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
}
</style>
