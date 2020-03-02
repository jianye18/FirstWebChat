<style>
  .container{
    /*background-color: #e5e5e5;*/
  }
  .swiper {
    height: 376rpx !important;
  }
  image {
    height: 100%;
    width: 100%;
  }
  .row_nav{
    height: 10px;
    background-color: #e5e5e5;
  }
  .article_data{
    font-size: 20px;
  }
  .article_div{
    border-bottom: 1px solid #e2e2e2;
  }
  .article_title{
    font-size: 20px;
    max-height: 48px;
    overflow: hidden;
    text-overflow: ellipsis;
    padding: 8px;
    border-bottom: 1px solid #e2e2e2;
  }
  .article_content{
    height: 30px;
    line-height: 30px;
  }
  .article_detail{
    text-align: center;
    color: #8E8E8E;
  }
  .article_type{
    width: 49%;
    float: left;
    border-right: 1px solid #e2e2e2;
  }
  .article_time{
    width: 50%;
    float: right;
  }
</style>
<template>
  <div class="container">
    <i-notice-bar icon="systemprompt" loop>
      2018年世界杯,将于6月14日至7月15日举行;2018年世界杯,将于6月14日至7月15日举行;
    </i-notice-bar>
    <view>
      <swiper class="swiper" :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration">
        <block v-for="(item, index) in bannerList" :key="index">
          <swiper-item>
            <image :src="item.path" class="slide-image" mode="aspectFill"/>
          </swiper-item>
        </block>
      </swiper>
    </view>
    <!--<i-grid>
      <i-grid-item @click="toList('LW')">
        <i-grid-icon>
          <i-icon type="activity" size="28" color="#80848f" />
        </i-grid-icon>
        <i-grid-label>法规</i-grid-label>
      </i-grid-item>
      <i-grid-item @click="toList('CC')">
        <i-grid-icon>
          <i-icon type="activity" size="28" color="#80848f" />
        </i-grid-icon>
        <i-grid-label>标准</i-grid-label>
      </i-grid-item>
    </i-grid>
    <i-grid>
      <i-grid-item @click="toList('SC')">
        <i-grid-icon>
          <i-icon type="activity" size="28" color="#80848f" />
        </i-grid-icon>
        <i-grid-label>抽检</i-grid-label>
      </i-grid-item>
      <i-grid-item @click="toList('FC')">
        <i-grid-icon>
          <i-icon type="activity" size="28" color="#80848f" />
        </i-grid-icon>
        <i-grid-label>飞检</i-grid-label>
      </i-grid-item>
    </i-grid>-->
    <!--<div style="border-bottom: 1px solid #e5e5e5; height: 40px; line-height: 40px;">
      <span style="height: 40px; line-height: 40px; font-size: 20px; margin-left: 10px;">最新文章</span>
      <span style="float: right; padding-right: 10px; color: #B9B9B9; line-height: 40px;" @click="toList('AC')">more</span>
    </div>
    <i-cell-group>
      <i-cell
        i-class="article_content"
        v-for="(item ,index) in newArticleList"
        :key="index"
        :title="item.title"
        @click="viewArticle(item.id)"></i-cell>
    </i-cell-group>-->
    <div v-for="(item, index) in newArticleList" v-bind:class="[index < newArticleList.length ? 'article_div' : '']">
      <div class="article_title">
        {{item.title}}
      </div>
      <div class="article_content">
        <div class="article_detail article_type">{{item.typeName}}</div>
        <div class="article_detail article_time">{{item.publishTime}}</div>
      </div>
    </div>
  </div>
</template>
<script>
// 导入 click-counter 组件
import ClickCounter from '@/components/click-counter/click-counter'
import globalStore from '../../stores/global-store'
export default {
  // 声明在当前组件下使用 counter-click 组件
  components: { ClickCounter },
  data () {
    return {
      msg: 'Hello',
      bannerList: [],
      resourcesBasePath: globalStore.state.resourcesBasePath,
      indicatorDots: true,
      vertical: false,
      autoplay: false,
      circular: false,
      interval: 2000,
      duration: 500,
      previousMargin: 0,
      nextMargin: 0,
      newArticleList: []
    }
  },
  computed: {
    count () {
      return globalStore.state.count
    }
  },
  mounted () {
    wx.showShareMenu()
    this.getHomeArticleList()
    this.getViewBannerList()
  },
  methods: {
    clickHandle () {
      this.msg = 'Clicked!!!!!!'
    },
    handleClickNum (data) {
      console.log('>>>>>>', data.num)
    },
    getHomeArticleList () {
      const _this = this
      this.$http.get({
        url: '/api/show/getHomeArticleList/?limit=10&orderName=create_time'
      }).then(res => {
        _this.newArticleList = res.data
        console.log(_this.newArticleList)
      })
    },
    getViewBannerList () {
      const _this = this
      this.$http.post({
        url: '/api/show/getViewBannerList',
        data: {isView: 1, limit: 5}
      }).then(res => {
        res.data.forEach(function (item) {
          _this.bannerList.push({ id: item.id, path: _this.resourcesBasePath + item.path + item.name, link: item.link })
        })
        console.log(_this.bannerList)
      })
    },
    getLinkViewList () {
      this.$http.get({
        url: '/api/show/getShowCount/1'
      }).then(res => {
        console.log(res)
      })
    },
    toList (type) {
      console.log(type)
      const url = '../list/main?type=' + type
      mpvue.navigateTo({ url })
    },
    viewArticle (id) {
      console.log('查看文章内容:' + id)
      const url = '../article/main?id=' + id
      mpvue.navigateTo({ url })
    }
  }
}
</script>
