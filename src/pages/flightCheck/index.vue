<template>
  <div class="container">
    <div style="width: 350px; margin: 10px auto;">
      <img src="../../../static/images/ad.png" style="width: 100%; height: 120px;" />
    </div>
    <view>
      <input class="search_text" type="text" placeholder="请输入搜索关键字" confirm-type="search" @confirm="search" />
    </view>
    <div class="table_title">
      {{flightCheck.businessName}}
    </div>
    <view class="tableView">
      <!-- <block> 并不是一个组件，它仅仅是一个包装元素，不会在页面中做任何渲染，只接受控制属性。 -->
      <block>
        <view class="table_cell">
          <view class="td td1">飞检类型</view>
          <view class="td td2">{{flightCheck.type}}</view>
        </view>
      </block>
      <block>
        <view class="table_cell">
          <view class="td td1">发布单位</view>
          <view class="td td2">{{flightCheck.publishUnit}}</view>
        </view>
      </block>
      <block>
        <view class="table_cell">
          <view class="td td1">发布时间</view>
          <view class="td td2">{{flightCheck.publishDate}}</view>
        </view>
      </block>
      <block>
        <view class="table_cell">
          <view class="td td1">是否有缺陷</view>
          <view class="td td2">{{flightCheck.isDefect}}</view>
        </view>
      </block>
      <block>
        <view class="table_cell">
          <view class="td td1">处理措施</view>
          <view class="td td2">{{flightCheck.precautions}}</view>
        </view>
      </block>
      <block>
        <view class="table_cell">
          <view class="td td1">问题内容</view>
          <view class="editor_content td2">
            <rich-text :nodes="flightCheck.problem" bindtap="tap" style="font-size: 12px;"></rich-text>
          </view>
        </view>
      </block>
      <block>
        <view class="table_cell">
          <view class="td td1">来源链接</view>
          <view class="td td2">{{flightCheck.sourceLink}}</view>
        </view>
      </block>
    </view>
  </div>
</template>
<script>
import '../accets/table.css'
export default {
  data () {
    return {
      currentId: null,
      flightCheck: {}
    }
  },
  mounted () {
    this.currentId = this.$root.$mp.query.id
    wx.showShareMenu()
    this.getFlightCheckById()
  },
  methods: {
    search (event) {
      const url = '../list/main?type=FC&&searchPhrase=' + event.target.value
      mpvue.navigateTo({ url })
      console.log(event.target.value)
    },
    getFlightCheckById () {
      const _this = this
      this.$http.get({
        url: '/api/flightCheck/getFlightCheckById/' + this.currentId
      }).then(res => {
        _this.flightCheck = res.data
        console.log(_this.flightCheck)
      })
    }
  }
}
</script>
