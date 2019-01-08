<template>
  <div id="wrapper">
         <Button @click="pu1">SystemInformation</Button>
        <Button @click="pu2">Manage</Button>
  </div>
</template>

<script>
  import SystemInformation from './LandingPage/SystemInformation'
  export default {
    name: 'landing-page',
    components: { SystemInformation },
    methods: {
      open (link) {
        this.$electron.shell.openExternal(link)
      },
      pu1 () {
        this.$router.push({path: '/SystemInformation'})
        console.log(this.$router.params)
      },
      pu2 () {
        this.$router.push({path: '/Manage'})
        console.log(this.$router.params)
      }
    }
  }
</script>

<style>
</style>
