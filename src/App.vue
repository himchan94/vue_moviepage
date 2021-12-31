<template>
  <div id="app">
    <ul class="header">
      <li class="ticket active" v-on:click="sortByTicket">예매순</li>
      <li class="star" v-on:click="sortByStar">평점순</li>
      <li class="start" v-on:click="sortByStart">개봉일순</li>
      <li class="viewer" v-on:click="sortByViewer">주말관객순</li>
      <li class="download" v-on:click="sortByDownload">다운로드순</li>
    </ul>

    <MovieList
      v-bind:movie-array="currentArr"
      v-bind:current-status="currentStatus"
    ></MovieList>
  </div>
</template>

<script>
import MovieList from "./components/MovieList.vue";

export default {
  name: "App",
  components: { MovieList },
  data() {
    return {
      currentArr: [],
      currentStatus: "예매순",
      rateMach: {
        0: "전체관람가",
        12: "12세이상 관람가",
        15: "15세이상 관람가",
        19: "19세이상 관람가",
        20: "청소년관람불가",
      },
      movies: [
        {
          name: "남애의 여름밤",
          src: "images/mov_1.jpg",
          rate: 15,
          score: 9.43, //평점
          sale: 11.7, //판매율
          openDate: 8.26, //개봉일
          ticketing: 11.79, //예매율
          week: 8777, //주말관객
        },
        {
          name: "시크릿 가든",
          src: "images/mov_2.jpg",
          rate: 0,
          score: 8.13,
          sale: 7.7, //판매율
          openDate: 9.3, //개봉일
          ticketing: 20.66,
          week: 2000,
        },
        {
          name: "반도",
          src: "images/mov_3.jpg",
          rate: 15,
          score: 8.54,
          sale: 7.7,
          openDate: 9.3,
          ticketing: 9.79,
          week: 23327,
        },
        {
          name: "강철비2",
          src: "images/mov_4.jpg",
          rate: 19,
          score: 7.43,
          sale: 7.7,
          openDate: 9.7,
          ticketing: 8.6,
          week: 23421,
        },
        {
          name: "신혼여행 허리케인",
          src: "images/mov_5.jpg",
          rate: 12,
          score: 6.2,
          sale: 10.7,
          openDate: 8.17,
          ticketing: 2.11,
          week: 3213,
        },
        {
          name: "테넷",
          src: "images/mov_6.jpg",
          rate: 19,
          score: 7.12,
          sale: 9.11,
          openDate: 11.17,
          ticketing: 3.21,
          week: 3213,
        },
        {
          name: "오케이 마담",
          src: "images/mov_7.jpg",
          rate: 20,
          score: 9.43,
          sale: 9.11,
          openDate: 9.1,
          ticketing: 3.79,
          week: 2277,
        },
        {
          name: "다만 악에서 구하소서",
          src: "images/mov_8.jpg",
          rate: 20,
          score: 8.9,
          sale: 8.8,
          openDate: 8.21,
          ticketing: 12.79,
          week: 83777,
        },
      ],
    };
  },
  mounted() {
    console.log("mounted");
    this.sortByTicket();
  },
  methods: {
    sortByTicket() {
      const newList = this.movies.sort((a, b) => b.ticketing - a.ticketing);
      this.currentArr = newList;
      this.currentStatus = "예매순";
      this.setActive("ticket");
    },
    sortByStart() {
      const newList = this.movies.sort((a, b) => b.openDate - a.openDate);
      this.currentArr = newList;
      this.currentStatus = "개봉일순";
      this.setActive("start");
    },
    sortByViewer() {
      const newList = this.movies.sort((a, b) => b.week - a.week);
      this.currentArr = newList;
      this.currentStatus = "주말관객순";
      this.setActive("viewer");
    },
    sortByDownload() {
      const newList = this.movies.sort((a, b) => b.sale - a.sale);
      this.currentArr = newList;
      this.currentStatus = "다운로드순";
      this.setActive("download");
    },
    sortByStar() {
      const newList = this.movies.sort((a, b) => b.score - a.score);
      this.currentArr = newList;
      this.currentStatus = "평점순";
      this.setActive("star");
    },
    setActive(cl) {
      const active = document.querySelector(".active");
      if (active) {
        active.classList.remove("active");
      }

      const selected = document.querySelector(`.${cl}`);
      selected.classList.add("active");
    },
  },
};
</script>


<style>
@charset 'utf-8';

/* reset */
body {
  font: normal 12px Arial, sans-serif;
  line-height: 1.3;
  color: #666666;
  background-color: #fff;
  margin: 0;
  padding: 0;
}
h1,
h2,
h3,
h4,
h5,
h6 {
  font-size: 1em;
}
h1,
h2,
h3,
h4,
h5,
h6,
div,
p,
dl,
dt,
dd,
ul,
ol,
li,
form,
fieldset,
blockquote,
address,
table,
thead,
tbody,
tfoot,
tr,
td,
caption {
  margin: 0;
  padding: 0;
}
li {
  list-style: none;
}
a {
  text-decoration: none;
  color: white;
}

/* movie */
body {
  background-color: #242424;
}

.header {
  overflow: hidden;
  font-size: 16px;
  display: flex;
  justify-content: center;
  margin-top: 30px;
}

.header > li {
  float: left;
  margin-left: 2.5rem;
  font-weight: bold;
  color: #fff;
}

.header > li.active {
  color: red;
}
</style>
