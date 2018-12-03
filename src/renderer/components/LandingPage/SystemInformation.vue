<template>
  <div>
    <Button @click="loadfile()">上传</Button>
    <Menu theme="light">
                <Submenu name="1">
                    <template slot="title">
                        <Icon type="ios-paper" />
                        {{PrjInfos}}
                    </template>
                    <MenuItem  v-for="(name,index) in NameItmes" :name="indexnames">{{index+1}}</MenuItem>
                    <MenuItem name="1-2">评论管理</MenuItem>
                    <MenuItem name="1-3">举报管理</MenuItem>
                </Submenu>
            </Menu>

  </div>
</template>

<script>
  import fs from 'fs'
  // import nedb from 'nedb'
  export default {
    data () {
      return {
        NameItmes: '',
        PrjInfos: '',
        indexname: ''
      }
    },
    methods: {
      loadfile () {
        this.$electron.ipcRenderer.send('loadfile')
        const _this = this
        this.$electron.ipcRenderer.on('filepath', function (event, arg) {
          console.log(arg[0])
          let filejson = JSON.parse(fs.readFileSync(arg[0], 'utf-8'))
          _this.NameItmes = filejson.item
          _this.PrjInfos = filejson.info.name
        })
      }
    },
  }
</script>

<style scoped>
  .title {
    color: #888;
    font-size: 18px;
    font-weight: initial;
    letter-spacing: .25px;
    margin-top: 10px;
  }

  .items { margin-top: 8px; }

  .item {
    display: flex;
    margin-bottom: 6px;
  }

  .item .name {
    color: #6a6a6a;
    margin-right: 6px;
  }

  .item .value {
    color: #35495e;
    font-weight: bold;
  }
</style>
