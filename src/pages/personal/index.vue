<template>
  <div class="container">
    <div class="headDiv">
      <div class="head_photo">
        <i-avatar size="large"><open-data type="userAvatarUrl"></open-data></i-avatar>
      </div>
      <div class="head_name"><open-data type="userNickName"></open-data></div>
      <div class="head_content">监督产品质量，人人参与，既是权力也是义务。</div>
    </div>
    <div>
      <i-cell-group>
        <i-cell title="我的积分">
          <i-icon slot="icon" type="mine_fill" size="28"/>
          <text slot="footer">0</text>
        </i-cell>
        <i-cell title="个人信息" is-link url="/pages/userInfo/main">
          <i-icon slot="icon" type="businesscard" size="28"/>
        </i-cell>
        <i-cell title="会员类别">
          <i-icon slot="icon" type="scan" size="28"/>
          <text slot="footer">普通会员</text>
        </i-cell>
        <i-cell title="关于博客" is-link url="/pages/about/main">
          <i-icon slot="icon" type="prompt" size="28"/>
        </i-cell>
      </i-cell-group>
    </div>
  </div>
</template>
<script>
  export default {
    data () {
      return {
        currentId: null
      }
    },
    mounted () {
      wx.showShareMenu()
    },
    methods: {
      toUserInfo () {
        const url = '../userInfo/main'
        mpvue.navigateTo({ url })
      }
    }
  }
</script>
<style>
  .headDiv{
    width: 100%;
    height: 200px;
    background-color: #e2e2e2;
  }
  .head_photo{
    height: 100px;
    line-height: 100px;
    text-align: center;
  }
  .head_name{
    text-align: center;
    height: 50px;
    line-height: 50px;
  }
  .head_content{
    font-size: 12px;
    text-align: center;
    height: 50px;
    line-height: 30px;
  }
</style>
