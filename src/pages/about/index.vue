<template>
  <div class="container">
    <statement/>
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
