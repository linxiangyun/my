<template>
    <div class="layout">
        <Layout>
            <Header>
                <Button @click="loadfile()">上传</Button>
            </Header>
            <Layout>
                <Sider hide-trigger :style="{background: '#fff'}">
                    <Menu active-name="1-2" theme="light" width="auto" :open-names="['1']">
                         <Submenu name="1">
                    <template slot="title">
                        <Icon type="ios-paper" />
                        {{PrjInfos}}
                    </template>
                    <MenuItem  v-for="(item,index) in NameItmes" :name="indexnames(index)">{{item.name}}</MenuItem>
                </Submenu>
                    </Menu>
                </Sider>
                <Layout :style="{padding: '0 24px 24px'}">
                    <Content :style="contstyle">
                        <Input search enter-button="Send" placeholder="Enter something..." />
                    </Content>
                </Layout>
            </Layout>
        </Layout>
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
        contstyle: {padding: '24px', minHeight: '500px', background: '#fff', position: ''}
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
      },
      indexnames: function (index) {
        return '1' + String(index + 1)
      }
    }
  }
</script>

<style scoped>
.layout{
    border: 1px solid #d7dde4;
    position: absolute;
    border-radius: 4px;
    overflow: hidden;
}
.layout-logo{
    width: 100px;
    height: 30px;
    border-radius: 3px;
    float: left;
    position: relative;
    top: 15px;
    left: 20px;
}
.layout-nav{
    width: 420px;
    margin: 0 auto;
    margin-right: 20px;
}
