<template>
  <view class="statement_data">
    <rich-text :nodes="statement" bindtap="tap" style="font-size: 14px;"></rich-text>
  </view>
</template>
<script>
export default {
  data () {
    return {
      statement: ''
    }
  },
  mounted () {
    this.getOneViewStatement()
  },
  methods: {
    getOneViewStatement () {
      const _this = this
      this.$http.get({
        url: '/api/show/getOneViewStatement'
      }).then(res => {
        _this.statement = res.data.content
        console.log(_this.statement)
      })
    }
  }
}
</script>
<style>
.statement_data {
  width: 350px;
  margin: 10px auto 0;
}
</style>
