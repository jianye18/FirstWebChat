<template>
  <div class="container">
    <div style="width: 350px; margin: 10px auto;">
      <img src="../../../static/images/ad.png" style="width: 100%; height: 120px;" />
    </div>
    <view>
      <input class="search_text" type="text" placeholder="请输入搜索关键字" confirm-type="search" @confirm="search" />
    </view>
    <div class="table_title">
      {{criterion.name}}
    </div>
    <view class="tableView">
      <!-- <block> 并不是一个组件，它仅仅是一个包装元素，不会在页面中做任何渲染，只接受控制属性。 -->
      <block>
        <view class="table_cell">
          <view class="td td1">标准状态</view>
          <view class="td td2">{{criterion.statusName}}</view>
        </view>
      </block>
      <block>
        <view class="table_cell">
          <view class="td td1">标准分类</view>
          <view class="td td2">{{criterion.categoryName}}</view>
        </view>
      </block>
      <block>
        <view class="table_cell">
          <view class="td td1">发布单位</view>
          <view class="td td2">{{criterion.publishUnitName}}</view>
        </view>
      </block>
      <block>
        <view class="table_cell">
          <view class="td td1">发布日期</view>
          <view class="td td2">{{criterion.publishDate}}</view>
        </view>
      </block>
      <block>
        <view class="table_cell">
          <view class="td td1">实施日期</view>
          <view class="td td2">{{criterion.implementDate}}</view>
        </view>
      </block>
      <block>
        <view class="table_cell">
          <view class="td td1">摘要</view>
          <view class="editor_content td2">
            <rich-text :nodes="criterion.summary" bindtap="tap" style="font-size: 12px;"></rich-text>
          </view>
        </view>
      </block>
      <!--<block>
        <view class="table_cell">
          <view class="td td1">附件</view>
          <view class="td td2">{{criterion.annexList}}</view>
        </view>
      </block>-->
    </view>
    <statement/>
  </div>
</template>
<script>
import statement from '@/components/statement/statement'
import '../accets/table.css'
export default {
  components: {
    statement
  },
  data () {
    return {
      currentId: null,
      criterion: {}
    }
  },
  mounted () {
    this.currentId = this.$root.$mp.query.id
    wx.showShareMenu()
    this.getCriterionById()
  },
  methods: {
    search (event) {
      const url = '../list/main?type=CC&&searchPhrase=' + event.target.value
      mpvue.navigateTo({ url })
      console.log(event.target.value)
    },
    getCriterionById () {
      const _this = this
      this.$http.get({
        url: '/api/criterion/getCriterionById/' + this.currentId
      }).then(res => {
        _this.criterion = res.data
        console.log(_this.criterion)
      })
    }
  }
}
</script>
