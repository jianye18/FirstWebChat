<template>
  <div class="container">
    <div style="width: 350px; margin: 10px auto;">
      <img src="../../../static/images/ad.png" style="width: 100%; height: 120px;" />
    </div>
    <view>
      <input class="search_text" type="text" placeholder="请输入搜索关键字" confirm-type="search" @confirm="search" />
    </view>
    <div class="table_title">
      {{spotCheck.sample}}
    </div>
    <view class="tableView">
      <!-- <block> 并不是一个组件，它仅仅是一个包装元素，不会在页面中做任何渲染，只接受控制属性。 -->
      <block>
        <view class="table_cell">
          <view class="td td1">标称委托企业</view>
          <view class="td td2">{{spotCheck.company}}</view>
        </view>
      </block>
      <block>
        <view class="table_cell">
          <view class="td td1">标称生产企业/进口代理商名称</view>
          <view class="td td2">{{spotCheck.producer}}</view>
        </view>
      </block>
      <block>
        <view class="table_cell">
          <view class="td td1">被采样单位名称</view>
          <view class="td td2">{{spotCheck.unit}}</view>
        </view>
      </block>
      <block>
        <view class="table_cell">
          <view class="td td1">公布日期</view>
          <view class="td td2">{{spotCheck.publishDate}}</view>
        </view>
      </block>
      <block>
        <view class="table_cell">
          <view class="td td1">包装规格</view>
          <view class="td td2">{{spotCheck.specification}}</view>
        </view>
      </block>
      <block>
        <view class="table_cell">
          <view class="td td1">保质期</view>
          <view class="td td2">{{spotCheck.expireTime}}</view>
        </view>
      </block>
      <block>
        <view class="table_cell">
          <view class="td td1">抽检结果</view>
          <view class="td td2">{{spotCheck.checkResult}}</view>
        </view>
      </block>
      <block>
        <view class="table_cell">
          <view class="td td1">不合格项目</view>
          <view class="td td2">{{spotCheck.subject}}</view>
        </view>
      </block>
      <block>
        <view class="table_cell">
          <view class="td td1">产品分类</view>
          <view class="td td2">{{spotCheck.productType}}</view>
        </view>
      </block>
      <block>
        <view class="table_cell">
          <view class="td td1">产地</view>
          <view class="td td2">{{spotCheck.location}}</view>
        </view>
      </block>
      <block>
        <view class="table_cell">
          <view class="td td1">涉嫌假冒</view>
          <view class="td td2">{{spotCheck.isFake}}</view>
        </view>
      </block>
      <block>
        <view class="table_cell">
          <view class="td td1">来源链接</view>
          <view class="td td2">{{spotCheck.sourceLink}}</view>
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
      spotCheck: {}
    }
  },
  mounted () {
    this.currentId = this.$root.$mp.query.id
    wx.showShareMenu()
    this.getSpotCheckById()
  },
  methods: {
    search (event) {
      const url = '../list/main?type=SC&&searchPhrase=' + event.target.value
      mpvue.navigateTo({ url })
      console.log(event.target.value)
    },
    getSpotCheckById () {
      const _this = this
      this.$http.get({
        url: '/api/spotCheck/getSpotCheckById/' + this.currentId
      }).then(res => {
        _this.spotCheck = res.data
        console.log(_this.spotCheck)
      })
    }
  }
}
</script>
