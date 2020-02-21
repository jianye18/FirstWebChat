<template>
  <div class="container">
    <i-tabs :current="current" @change="handleChange">
      <i-tab i-class="tab_item" key="LW" title="法规"></i-tab>
      <i-tab i-class="tab_item" key="CC" title="标准"></i-tab>
      <i-tab i-class="tab_item" key="SC" title="抽检"></i-tab>
      <i-tab i-class="tab_item" key="FC" title="飞检"></i-tab>
      <i-tab i-class="tab_item" key="AC" title="文章"></i-tab>
    </i-tabs>
    <!--<i-input title="搜索框" placeholder="请输入搜索关键字" mode="wrapped" />-->
    <!--<i-panel title="">
      <input type="text" placeholder="请输入搜索关键字" confirm-type="search" @confirm="search"/>
    </i-panel>-->
    <view>
      <input type="text" placeholder="请输入搜索关键字" v-model="formData.searchPhrase" confirm-type="search" @confirm="search" class="search_text"/>
    </view>
    <!--<i-cell-group i-class="list_content">
      <i-cell
        i-class="content"
        v-for="(item ,index) in dataList"
        :key="index" :title="item.title" :value="item.publishTime"
        @click="viewArticle(item.id)">
      </i-cell>
    </i-cell-group>-->
    <view v-for="(item ,index) in dataList" :key="index" @click="viewArticle(item.id)" class="list_content">
      <view class="list_item list_title">{{item.title}}</view>
      <view class="list_item list_time">{{item.publishTime}}</view>
    </view>
  </div>
</template>
<script>
  export default {
    data () {
      return {
        scrollTop: 0,
        current: '',
        maskShow: true,
        dataList: [],
        formData: {
          orderName: 'publish_date',
          orderType: 'desc',
          pageNum: 1,
          pageSize: 20,
          searchPhrase: ''
        },
        isPullDownRefresh: false
      }
    },
    mounted () {
      this.current = this.$root.$mp.query.type
      this.formData.searchPhrase = this.$root.$mp.query.searchPhrase || ''
      wx.showShareMenu()
      this.getListData()
    },
    methods: {
      // 页面滚动执行方式
      onPageScroll (event) {
        this.scrollTop = event.scrollTop
      },
      handleChange (res) {
        console.log(res)
        this.current = res.target.key
        this.formData = {
          orderName: 'publish_date',
          orderType: 'desc',
          pageNum: 1,
          pageSize: 10,
          searchPhrase: ''
        }
        this.getListData()
      },
      getListData () {
        const _this = this
        let url = ''
        if (_this.current === 'AC') {
          _this.formData.orderName = 'publish_time'
          _this.formData.isPublish = 1
          url = '/api/article/getArticlePageList'
        }
        if (_this.current === 'SC') {
          _this.formData.orderName = 'publish_date'
          url = '/api/spotCheck/getSpotCheckPageList'
        }
        if (_this.current === 'CC') {
          _this.formData.orderName = 'implement_date'
          url = '/api/criterion/getCriterionPageList'
        }
        if (_this.current === 'FC') {
          _this.formData.orderName = 'publish_date'
          url = '/api/flightCheck/getFlightCheckPageList'
        }
        if (_this.current === 'LW') {
          _this.formData.orderName = 'implement_date'
          url = '/api/law/getLawPageList'
        }
        _this.$http.post({
          url: url,
          data: _this.formData
        }).then(res => {
          if (res.code === 200) {
            if (_this.formData.pageNum === 1) {
              _this.dataList = res.data.list
            } else {
              _this.dataList = _this.dataList.concat(res.data.list)
            }
            if (_this.isPullDownRefresh) {
              // 隐藏导航栏加载框
              wx.hideNavigationBarLoading()
              // 停止下拉动作
              wx.stopPullDownRefresh()
            }
          }
          console.log(_this.dataList)
        })
      },
      search (event) {
        // this.formData.searchPhrase = event.target.value
        this.formData.pageNum = 1
        this.getListData()
      },
      viewArticle (id) {
        console.log('跳转详情页:' + id)
        if (this.current === 'AC') {
          const url = '../article/main?id=' + id
          mpvue.navigateTo({ url })
        }
        if (this.current === 'SC') {
          const url = '../spotCheck/main?id=' + id
          mpvue.navigateTo({ url })
        }
        if (this.current === 'CC') {
          const url = '../criterion/main?id=' + id
          mpvue.navigateTo({ url })
        }
        if (this.current === 'FC') {
          const url = '../flightCheck/main?id=' + id
          mpvue.navigateTo({ url })
        }
        if (this.current === 'LW') {
          const url = '../law/main?id=' + id
          mpvue.navigateTo({ url })
        }
      }
    },
    onPullDownRefresh () {
      // 显示顶部刷新图标
      wx.showNavigationBarLoading()
      this.isPullDownRefresh = true
      this.formData = {
        orderName: 'publish_date',
        orderType: 'desc',
        pageNum: 1,
        pageSize: 10,
        searchPhrase: ''
      }
      this.getListData()
    },
    onReachBottom () {
      // 显示加载图标
      wx.showLoading({
        title: '玩命加载中'
      })
      this.formData.pageNum = this.formData.pageNum + 1
      this.getListData()
    }
  }
</script>
<style>
  .cover-view {
    position: fixed;
    /*top: calc(50% - 150rpx);
    left: calc(50% - 300rpx);*/
    right: 10px;
    bottom: 10px;
    /* opacity: .7; */
  }
  .flex-item{
    width: 50rpx;
    height: 50rpx;
    font-size: 26rpx;
  }
  .tab_item .i-tabs-tab-title{
    font-size: 16px;
  }
  .list_content{
    display: flex;
    flex-direction:row;
    justify-content: start;
    border: 0 solid #e9eaec;
    border-bottom-width: 1px;
  }
  .list_item{
    line-height: 40px;
    font-size: 14px;
  }
  .list_title{
    padding-left: 15px;
    width: 70%;
  }
  .list_time{
    width: 25%;
    margin-left: 5%;
  }
  .search_text{
    width: 350px;
    height: 35px;
    border: 1px solid #e2e2e2;
    border-radius: 5px;
    margin: 10px auto;
    padding-left: 5px;
  }
</style>
