<template>
  <div class="NewsList">
    <div class="container">

      <ul class="media-list">
        <li class="media" v-for="article in articles">
          <div class="media-left">

            <a v-bind:href="article.url" target="_blank">
              <img class="media-object" src="article.urlToImage">
            </a>
          </div>
          <div class="media-body">
            <h4 class="media-heading">
              <a v-bind:href="article.url" target="_blank">{{article.title}}</a></h4>
            <h5>
              <i>by {{article.author}}</i></h5>
            <p>{{article.description}}</p>


          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
  export default {
    name: "NewsList",
    props: ['source'],
    data() {
      return {
        articles: []
      }

    },
    methods: {
      updateSource: function (newVal) {
        this.$http.get('https://newsapi.org/v1/articles?source=' + newVal + '&apiKey=ea0d316021994e81aa2c50c18bdff3f6').then(response => {
          this.articles = response.data.articles;
        })
      }
    },
    created: function () {
      this.updateSource(this.source);

    },
    watch: {
      source: function (newVal) {

        this.updateSource(newVal);

      }
    }
  }
</script>

<style scoped>

  .media-object {
    width: 128px;
    padding: 10px;
  }

  .media {
    border-top: 1px solid lightgoldenrodyellow;
    padding-top: 20px;

  }

</style>
