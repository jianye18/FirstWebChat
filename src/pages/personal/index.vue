<template>
  <div class="container">
    <div class="headDiv">
      <div class="head_photo">
        <i-avatar size="large">叶</i-avatar>
      </div>
      <div class="head_name">叶竹洪</div>
      <div class="head_content">监督产品质量，人人参与，既是权力也是义务。</div>
    </div>
    <div>
      <i-cell-group>
        <i-cell title="我的积分" icon="mine_fill" is-link>
          <i-icon slot="icon" type="mine_fill" size="28"/>
        </i-cell>
        <i-cell title="个人信息" icon="mine_fill" is-link>
          <i-icon slot="icon" type="businesscard" size="28"/>
        </i-cell>
        <i-cell title="会员类别" icon="mine_fill" is-link>
          <i-icon slot="icon" type="scan" size="28"/>
        </i-cell>
        <i-cell title="关于博客" icon="mine_fill" is-link>
          <i-icon slot="icon" type="prompt" size="28"/>
        </i-cell>
      </i-cell-group>
    </div>
  </div>
</template>
<script>
  import statement from '@/components/statement/statement'
  export default {
    components: {
      statement
    },
    data () {
      return {
        currentId: null
      }
    },
    mounted () {
      wx.showShareMenu()
    },
    methods: {
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
