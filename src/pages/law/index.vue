<style>
  .td view{
    text-align: left;
    padding: 1px;
  }
</style>
<template>
  <div class="container">
    <div style="width: 350px; margin: 10px auto;">
      <img src="../../../static/images/ad.png" style="width: 100%; height: 120px;" />
    </div>
    <view>
      <input class="search_text" type="text" placeholder="请输入搜索关键字" confirm-type="search" @confirm="search" />
    </view>
    <div class="table_title">
      {{law.name}}
    </div>
    <view class="tableView">
      <!-- <block> 并不是一个组件，它仅仅是一个包装元素，不会在页面中做任何渲染，只接受控制属性。 -->
      <block>
        <view class="table_cell">
          <view class="td td1">状态</view>
          <view class="td td2">{{law.statusName}}</view>
        </view>
      </block>
      <block>
        <view class="table_cell">
          <view class="td td1">发布单位</view>
          <view class="td td2">{{law.publishUnitName}}</view>
        </view>
      </block>
      <block>
        <view class="table_cell">
          <view class="td td1">文号</view>
          <view class="td td2">{{law.codeNumber}}</view>
        </view>
      </block>
      <block>
        <view class="table_cell">
          <view class="td td1">发布日期</view>
          <view class="td td2">{{law.publishDate}}</view>
        </view>
      </block>
      <block>
        <view class="table_cell">
          <view class="td td1">实施日期</view>
          <view class="td td2">{{law.implementDate}}</view>
        </view>
      </block>
      <block>
        <view>
          <view class="editor_content">
            <rich-text :nodes="law.content" bindtap="tap" style="font-size: 12px;"></rich-text>
          </view>
        </view>
      </block>
      <!--<block v-if="law.annexList">
        <view class="table_cell">
          <view class="td td1">附件</view>
          <view class="td td2">{{law.annexList}}</view>
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
      law: {}
    }
  },
  mounted () {
    this.currentId = this.$root.$mp.query.id
    wx.showShareMenu()
    this.getLawById()
  },
  methods: {
    search (event) {
      const url = '../list/main?type=LW&&searchPhrase=' + event.target.value
      mpvue.navigateTo({ url })
      console.log(event.target.value)
    },
    getLawById () {
      const _this = this
      this.$http.get({
        url: '/api/law/getLawById/' + this.currentId
      }).then(res => {
        _this.law = res.data
        console.log(_this.law)
      })
    }
  }
}
</script>
