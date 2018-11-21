<template>

  <div class="sourceSelection">
    <div class="jumbotron">
      <h2><span class="glyphicon glyphicon-list-alt"></span> News List</h2>
      <h4>Select a News Source:</h4>
      <select class="form-control" v-on:change="sourceChanged">
        <option v-bind:value="source.id" v-for="source in sources">{{source.name}}</option>
      </select>
      <div v-if="source">
        <h6>Selected News Source is {{source.description}}</h6>
        <a v-bind:href="source.url" class="btn btn-primary" target="_blank">Go To {{source.name}} website</a>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: "SourceSelection",
    data() {
      return {
        sources: [],
        source: ''
      }

    }, methods: {
      sourceChanged: function (param) {

        for (var i = 0; i < this.sources.length; i++) {
          if (this.sources[i].id == param.target.value) {
            this.source = this.sources[i];

          }
        }
        this.$emit('sourceChanged', param.target.value);

      }
    },
    created: function () {
      this.$http.get('https://newsapi.org/v2/sources?apiKey=ea0d316021994e81aa2c50c18bdff3f6&language=en').then(response => {
        this.sources = response.data.sources;
      })

    }


  }
</script>

<style scoped>

</style>


