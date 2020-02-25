<template>
  <div class="box">
    <h1>Articles</h1>
    <SourceSelection />
    <NewsList />
    <div>
      <div>
        <h3>Select News Source</h3>
        <select v-on:change="sourceChanged">
          <option>Please select news source</option>
          <option v-for="source in sources" 
            :key="source.id"
            :value="source.id">
            {{ source.name }}
            </option>
        </select>
      </div>
      <div v-for="article in articles" :key="article.id">
        <div class="media-left">
          <a :href="article.url">
            <img :src="article.urlToImage" />
          </a>
        </div>
        <div>
          <h2>{{ article.title }}</h2>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import SourceSelection from './SourceSelection';
import NewsList from './NewsList';

export default {
  name: "Home",
  components: {
    SourceSelection,
    NewsList
  },
  data: function() {
    return {
      articles: [],
      sources: []
    };
  },
  methods: {
    sourceChanged: async function(evt) {
      this.articles = await this.getArticles(evt.target.value);
    },
    getArticles: function(sourceId) {
      const newsApiEndpoint =
        "https://newsapi.org/v2/top-headlines";
      const apiKey = "039a82e7755f4ba2873a8614536d3e66";

      this.$http
        .get(`${newsApiEndpoint}?sources=${sourceId}&apiKey=${apiKey}`)
        .then(function(response) {
          this.articles = response.body.articles;
        });
    },

    getSources: function() {
      const sourcesEndPoint =
      "https://newsapi.org/v2/sources";
      const apiKey = "039a82e7755f4ba2873a8614536d3e66";

      this.$http
      .get(`${sourcesEndPoint}?apiKey=${apiKey}`)
      .then(function(sourceResponse) {
        this.sources = sourceResponse.body.sources;
      });
    }
  },

  created: function() {
    this.getArticles();
    this.getSources();
  }

};
</script>

<style scoped>
  .box {
    text-align: center;
  }

  h1 {
    font-family: sans-serif;
  }

  h3 {
    font-family: sans-serif;
  }

  img {
    margin-top: 20px;
    width: 50%;
  }
</style>