<template>
  <div>
    <div class="input-group mb-3">
      <input v-model="query" type="text" class="form-control" placeholder="Enter news query" />
      <div class="input-group-append">
        <button v-on:click="showResult" class="btn btn-outline-secondary" type="button">Search</button>
      </div>
    </div>

    <div class="articles">
      <ul v-if="this.articles">
        <li v-for="article in articles" :key="article.content">
          <div @click="openLink(article.url)" class="links">
            <h5>{{ article.content }}</h5>
            <p>
              {{ article.author }}
              <span>{{ new Date(article.publishedAt).toDateString()}}</span>
            </p>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "News",

  data() {
    return {
      query: "",
      articles: null,
    };
  },
  methods: {
    showResult: function () {
      axios(
        `https://newsapi.org/v2/everything?q=${this.query}&sortBy=popularity&apiKey=8b7ed73d8bb64d4da67648bb8d8525b3`
      )
        .then((res) => {
          this.articles = res.data.articles;
        })
        .catch((err) => console.log(err));
    },
    openLink: function (link) {
      window.open(link, "_blank");
    },
  },
};
</script>

<style>
li {
  list-style: none;
  text-align: justify;
  border: 1px solid grey;
  margin: 10px;
  padding: 20px;
  margin-top: 50px;
}

span {
  color: rebeccapurple;
}

.links {
  cursor: pointer;
}
</style>