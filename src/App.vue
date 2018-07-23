<template>
  <div id="app">
    <naver-list v-bind:top="title"></naver-list>
  </div>
</template>

<script>
  import HelloWorld from './components/HelloWorld'
  import cleanStr from './add_js/cleanString'
  import NaverList from './components/NaverList'
  import axios from 'axios'

  let clientId = "K99rkGyg42Jf0FBSTQgO";
  let clientSecret = "M0BbIqUL5F";


  export default {
    name: 'App',
    comments:{
      NaverList
    },
    data() {
      return {
        title: [],
        link: [],
        tophun: []
      }
    },
    mounted() {
      this.search();
    },
    methods: {
      search: function () {
        axios({
          method: "get",
          url: "/naversearch",
          params: {
            query: "세종대",
            display: "100"
          },
          crossDomain: true,
          headers: {
            "X-Naver-Client-Id": clientId,
            "X-Naver-Client-Secret": clientSecret
          }
        }).then((result) => {
          //console.log(result.data.items[50]);
          let news = result.data.items;
          for (let i in news) {
            console.log(news[i].title);
            this.title.push(cleanStr(news[i].title, "title"));
            this.link.push(cleanStr((news[i].originallink, "title")));
          }
        })
      }
    },
    components: {
      NaverList,
      HelloWorld
    }
  }
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
