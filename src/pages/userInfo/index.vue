<template>
  <div class="container">
    <!--<i-row>
      <i-col span="4" i-class="col-class">昵称</i-col>
      <i-col span="2" i-class="col-class"></i-col>
      <i-col span="18" i-class="col-class"><open-data type="userNickName"></open-data></i-col>
    </i-row>-->
    <i-cell-group>
      <i-cell title="头像">
        <i-avatar slot="footer" shape="square"><open-data type="userAvatarUrl"></open-data></i-avatar>
      </i-cell>
      <i-cell title="昵称">
        <open-data slot="footer" type="userNickName"></open-data>
      </i-cell>
      <i-cell title="性别">
        <open-data slot="footer" type="userGender" lang="zh_CN"></open-data>
      </i-cell>
      <i-cell title="城市">
        <open-data slot="footer" type="userCity" lang="zh_CN"></open-data>
      </i-cell>
    </i-cell-group>
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

</style>
