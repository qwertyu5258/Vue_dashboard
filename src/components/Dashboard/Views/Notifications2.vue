<template>
    <div id="app">
    <div v-if="hasResult">
      <div v-for="post in posts" v-bind:key="post.id">
        <h1></h1>
        <p></p>
      </div>
    </div>
    <button v-else v-on:click="searchTerm">글 불러오기</button>
    {{posts}}
<Br/><Br/><Br/><Br/>
<div v-if="posts!=''">
    {{posts[0].candleDateTimeKst}} <br/>
    {{posts[0].tradePrice}} BTC 
    <br/><br/><br/>
    {{posts2[0].candleDateTimeKst}} <br/>
    {{posts2[0].tradePrice}} ETH
</div>
  </div>
</template>
<script>
export default {
  name: 'app',
  data: function () {
    return {
      posts: [],
      posts2 : []
    }
  },
  computed: {
    hasResult: function () {
      return this.posts.length > 0
    }
  },
  methods: {
    searchTerm: function () {
      // using JSONPlaceholder
      const baseURI = 'https://crix-api-endpoint.upbit.com/v1/crix/candles/minutes/1?code=CRIX.UPBIT.KRW-BTC&count=10'
      const baseURI2 = 'https://crix-api-endpoint.upbit.com/v1/crix/candles/minutes/1?code=CRIX.UPBIT.KRW-ETH&count=10'
      this.$http.get(`${baseURI}`)
      .then((result) => {
        console.log(result)
        this.posts = result.data
      })
      this.$http.get(`${baseURI2}`)
      .then((result) => {
        console.log(result)
        this.posts2 = result.data
      })
    }
  }
}
</script>
<style lang="scss">

</style>
