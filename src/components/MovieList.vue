<template>
  <div class="movie">
    <ol class="list">
      <li v-for="(movie, i) in movieArray" v-bind:key="i">
        <a href="">
          <h4 class="hide">{{ movie.name }}</h4>
          <span v-bind:class="`hide rate rate${movie.rate}`"></span>
          <strong class="rank">{{ i + 1 }}</strong>
          <img
            class="poster"
            v-bind:src="require(`@/assets/${movie.src}`)"
            v-bind:alt="movie.title"
          />
          <template v-if="status === `예매순`">
            <span class="desc">
              <em class="score" style="color: red">{{ movie.ticketing }}%</em>
              <em>예매율</em>
            </span>
          </template>
          <template v-if="status === `개봉일순`">
            <span class="desc">
              <em>개봉</em>
              <em class="score" style="color: red">{{ movie.openDate }}</em>
            </span>
          </template>
          <template v-if="status === `평점순`">
            <span class="desc">
              <i class="star"
                ><b v-bind:style="`width: ${(movie.score / 10) * 100}%`"></b
              ></i>
              <em class="score">{{ movie.score }}</em>
            </span>
          </template>
          <template v-if="status === `다운로드순`">
            <span class="desc">
              <em class="score" style="color: red">{{ movie.sale }}%</em>
              <em>판매율</em>
            </span>
          </template>
          <template v-if="status === `주말관객순`">
            <span class="desc">
              <em>명</em>
              <em class="score" style="color: red">{{ movie.week }}</em>
            </span>
          </template>
        </a>
      </li>
    </ol>
  </div>
</template>

<script>
export default {
  data() {
    return {
      status: "예매순",
    };
  },
  props: ["movieArray", "currentStatus"],
  watch: {
    currentStatus() {
      this.status = this.currentStatus;
    },
  },
};
</script>

<style scoped>
.movie {
  width: 590px;
  margin: 5px auto 0;
  padding: 10px;
  background-color: #242424;
  overflow: hidden;
}
.movie > ol > li {
  float: left;
  width: 125px;
  height: 204px;
  margin: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.4);
  border: 1px solid rgba(255, 255, 255, 0.2);
}
.movie > ol > li a {
  display: block;
  position: relative;
}
.movie > ol > li .hide {
  font-size: 0;
}
.movie > ol > li .rank {
  position: absolute;
  top: 5px;
  left: 5px;
  font-size: 24px;
  font-style: italic;
  color: white;
  text-shadow: 0 0 10px black;
}
.movie > ol > li .rate {
  position: absolute;
  top: 5px;
  right: 5px;
  content: "";
  width: 25px;
  height: 25px;
  display: block;
  background-image: url("../assets/images/icon_rate.png");
  background-repeat: no-repeat;
}
.movie > ol > li .rate15 {
  background-position: 0 -60px;
}
.movie > ol > li .rate12 {
  background-position: 0 -30px;
}
.movie > ol > li .rate00 {
  background-position: 0 0;
}
.movie > ol > li .rate19 {
  background-position: 0 -120px;
}
.movie > ol > li .rate20 {
  background-position: 0 -90px;
}
.movie > ol > li .poster {
  display: block;
}
.movie > ol > li .desc {
  position: relative;
  background-color: black;
  display: block;
  height: 25px;
}
.movie > ol > li i {
  float: left;
  margin: 5px 0 0 10px;
  font-style: normal;
}
.movie > ol > li em {
  float: right;
  margin: 5px 10px 0 0;
  font-weight: bold;
  font-style: normal;
}
.movie > ol > li i.star {
  width: 71px;
  height: 14px;
  background: url("../assets/images/icon_star.png") no-repeat 0 0/71px auto;
}
.movie > ol > li i.star > b {
  display: block;
  width: 0;
  height: 100%;
  background: url("../assets/images/icon_star.png") no-repeat 0 -15px/71px auto;
}
.movie > ol > li i.reserv_title {
  font-weight: bold;
}
.movie > ol > li em.reserv_num {
  color: red;
}
.movie > ol > li i.open_title {
  position: absolute;
  right: 35px;
  font-weight: bold;
  color: red;
}
.movie > ol > li em.open_num {
  font-weight: bold;
}
.movie > ol > li i.week_title {
  font-weight: bold;
}
.movie > ol > li em.week_num {
  color: red;
}
.movie > ol > li i.sale_title {
  font-weight: bold;
}
.movie > ol > li em.sale_num {
  color: red;
}
.movie > .tab {
  text-align: center;
  font-size: 16px;
}
.movie > .tab > li {
  display: inline-block;
  margin: 0 20px;
}
.movie > .tab > li.on a {
  color: red;
}
</style>