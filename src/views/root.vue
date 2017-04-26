<template>
  <div class="main">
    <h2 class="title">热电厂二期项目</h2>
    <Input class="search" placeholder="搜索过滤建筑物名称" style="width: 100%"></Input>
    <h3 class="list"><i class="iconfont icon-viewgallery"></i> 单体建筑</h3>
    <building class="main-table" v-for="(building, index) in buildings" :building="building" :key="building.id">
    </building>
  </div>
</template>

<script>
  import building from './building/building.vue'

  export default {
    props: ['db'],
    data () {
      let buildings = this.db.buildings
      return {
        buildings: buildings
      }
    },
    components: {
      building
    }
  }
</script>

<style>
  @import "../common/css/base.css";
  @import '../common/css/iconfont.css';

  .main {
    margin: 25px;
  }

  .main .iconfont {
    font-weight: 700;
  }

  .title {
    font-size: 28px;
  }

  .list {
    font-size: 20px;
    margin: 15px 0;
  }

  .search input {
    margin: 15px 0;
    background: #f7f8f7;
  }

  .main-table {
    margin: 15px 0;
    background: #f7f8f7;
  }
</style>
