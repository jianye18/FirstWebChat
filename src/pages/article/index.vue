<template>
  <div class="container">
    <div class="table_title">
      {{article.title}}
    </div>
    <div style="font-size: 16px; padding: 5px 10px;">
      <span>作者：</span>
      <span>{{article.author}}</span>
      <span> 发布于：</span>
      <span>{{article.publishTime}}</span>
    </div>
    <view style="padding-left: 10px;">
      <rich-text :nodes="article.content" bindtap="tap" style="font-size: 36rpx;"></rich-text>
    </view>
  </div>
</template>
<script>
export default {
  data () {
    return {
      currentId: null,
      article: {}
    }
  },
  mounted () {
    this.currentId = this.$root.$mp.query.id
    wx.showShareMenu()
    this.getArticleById()
  },
  methods: {
    getArticleById () {
      const _this = this
      this.$http.get({
        url: '/api/article/getArticleById/' + this.currentId
      }).then(res => {
        _this.article = res.data
        console.log(_this.article)
      })
    }
  }
}
</script>
