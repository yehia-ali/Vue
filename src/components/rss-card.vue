<template>
  <li class="flex-item">
    <router-link :to="`/`">
      <img :src="data.enclosure.link" :alt="data.title" />
      <div class="overlay"></div>
      <div class="content">
        <h2>{{ data.title }}</h2>
        <p v-if="data.pubDate">{{ moment(data.pubDate).format('D/M/YYYY') }}</p>
      </div>
    </router-link>
  </li>
</template>

<style lang="scss">
ul {
  display: flex;
  flex-flow: row wrap;
  margin: auto;
  padding: 0;
  li {
    display: flex;
    align-items: flex-end;
    position: relative;
    min-width: 15rem;
    min-height: 15rem;
    list-style-type: none;
    margin: 1%;
    padding: 1%;
    width: 5rem;
    background: #776767;
    color: white;
    border-radius: 4px;
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.085), 0 1px 8px rgba(0, 0, 0, 0.8);
    transition: all 1s;
    &.flex-item {
      flex-grow: 1;
      &:nth-of-type(6n + 1) {
        flex: 1 58%;
      }
    }

    &:hover {
      box-shadow: 0 1px 8px rgba(0, 0, 0, 0.5), 0 8px 24px rgba(0, 0, 0, 0.8);
      transform: scale(1.05);
    }
    img {
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      margin: auto;
      width: 100%;
      height: 100%;
      object-fit: cover;
      border-radius: 4px;
    }
    a {
      color: #fff;
      text-decoration: none;
    }
    h2 {
      font-size: 18px;
      margin: 5px;
    }
    p {
      font-size: 14px;
      color: rgba(255, 255, 255, 0.5);
      margin: 5px;
    }
  }
  .overlay {
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    background: linear-gradient(180deg, rgba(0, 0, 0, 0) 39%, #000 100%);
  }
  .content {
    position: relative;
  }
}
</style>

<script>
import moment from 'moment';
export default {
  props: {
    data: {
      required: true
    },
  },
    methods: {
    moment: function (date) {
      return moment(date);
    },
    },
};
</script>
