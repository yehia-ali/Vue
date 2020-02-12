<template>
  <div>
    <div class="container" v-if="rsss">
      <app-header>
        <img :src="logo_header" alt="random image" />
        <h2>
          {{ title_header }}
        </h2>
      </app-header>
      <section>
        <ul>
          <rss-card v-for="rss in rsss" :key="rss.id" :data="rss"></rss-card>
        </ul>
      </section>
    </div>
    <div class="text-center">
      <button type="button" class="load-more-button" @click="loadMore">
        View More
      </button>
    </div>
  </div>
</template>

<script>
import AppHeader from "../components/app-header";
import rssCard from "../components/rss-card";
import axios from "axios";

export default {
  data() {
    return {
      title_header: null,
      logo_header: null,
      rsss: null,
      api_key: "f0woudedz1tyzn1upqfcclkfmqmzagflwwyjcyqp",
      totalCount: null,
      count: 7
    };
  },
  components: {
    AppHeader,
    rssCard
  },
  mounted() {
    this.getrsss();
  },
  methods: {
    getrsss() {
      axios
        .get(
          `https://api.rss2json.com/v1/api.json?rss_url=http://rss.cnn.com/rss/edition.rss&api_key=${this.api_key}&count=${this.count}`
        )
        .then(res => {
          this.rsss = res.data.items;
          this.totalCount = res.headers["x-total-count"];
          this.title_header = res.data.feed.title;
          this.logo_header = res.data.feed.image;
        });
    },
    loadMore() {
      this.count = this.count + 7;
      this.getrsss();
    }
  }
};
</script>

<style lang="scss">
.container {
  padding: 0 10px;
  max-width: 1024px;
  margin: auto;
  display: flex;
  flex-wrap: wrap;

  header {
    display: flex;
    align-items: center;
    img {
      margin-right: 10px;
    }
    h2 {
      font-size: 18px;
    }
  }
}
  .load-more-button {
    color: #000;
    border: 2px solid #000;
    border-radius: 5px;
    padding: 10px 25px;
    font-size: 18px;
    line-height: 1;
    margin-top: 50px;
    margin-bottom: 50px;
    background: transparent;
    cursor: pointer;
    transition: all 0.4s;
    &:hover {
      border: 2px solid #000;
      background: #000;
      color: #fff;
    }
  }
</style>
