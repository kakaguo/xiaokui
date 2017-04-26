<template>
  <div class="main">
    <h2 class="title">热电厂二期项目</h2>
    <Input class="search" placeholder="搜索过滤建筑物名称" style="width: 100%"></Input>
    <div class="main-table" v-for="building in buildings">
      <h3 class="name">{{ building.name }}</h3>
      <ul>
        <li>计划开始: {{ building.start_date | dateFormat}}</li>
        <li>计划完成: {{ building.end_date | dateFormat}}</li>
        <li>计划工期: {{ building.total_duration }}</li>
        <li>已经施工: {{ building.total_elapsed }}</li>

        <li>下面两个做成进度条</li>
        <li>计划进度: {{ building.plan_progress }}</li>
        <li>实际进度: {{ building.real_progress }}</li>
      </ul>

      <h4>分布工程</h4>
      <ul>
        <li v-for="part in building.parts">
          <ul>
            <li>计划开始: {{ part.start_date | dateFormat}}</li>
            <li>计划完成: {{ part.end_date | dateFormat}}</li>
            <li>计划工期: {{ part.total_duration }}</li>
            <li>已经施工: {{ part.total_elapsed }}</li>

            <li>下面两个做成进度条</li>
            <li>计划进度: {{ part.plan_progress }}</li>
            <li>实际进度: {{ part.real_progress }}</li>
          </ul>
        </li>
      </ul>
      <hr>
    </div>
  </div>
</template>

<script>
export default {
  props: ['db'],
  data () {
    let buildings = this.db.buildings

    return {
      buildings: buildings
    }
  }
}
</script>

<style>
  @import "../common/css/base.css";
  .main {
    margin: 25px;
  }

  .title {
    font-size: 28px;
  }

  .search input {
    margin: 15px 0;
    background: #f7f8f7;
  }

  .main .main-table {
    margin: 15px 0;
    background: #f7f8f7;
  }
</style>
