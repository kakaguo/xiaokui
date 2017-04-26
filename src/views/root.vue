<template>
  <div class="main">
    <h2 class="title">热电厂二期项目</h2>
    <Input class="search" placeholder="搜索过滤建筑物名称" style="width: 100%"></Input>
    <h3 class="list"><i class="iconfont icon-viewgallery"></i> 单体建筑</h3>
    <div class="main-table" v-for="building in buildings">
      <h3 class="name">{{ building.name }}</h3>
      <Row class="table">
        <Col span="6">
        计划开始<p>{{ building.start_date | dateFormat}}</p></Col>
        <Col span="6">
        计划完成<p>{{ building.end_date | dateFormat}}</p></Col>
        <Col span="6">
        计划工期<p>{{ building.total_duration }}天</p></Col>
        <Col span="6">
        已经施工<p>{{ building.total_elapsed }}天</p></Col>
      </Row>
      <ul>
        <progressbar :real="building.real_progress" :plan="building.plan_progress"></progressbar>
        <li>计划进度: {{ building.plan_progress }}</li>
        <li>实际进度: {{ building.real_progress }}</li>
      </ul>
      <div class="part">
        <h4 class="part-title"><i class="iconfont icon-similarproduct"></i> 分布工程</h4>
        <span class="part-icon part-unfold" v-show="detailShow"><i class="iconfont icon-moreunfold" @click="showDetail"></i></span>
        <span class="part-icon part-fold" v-show="detailShow"><i class="iconfont icon-less" @click="hideDetail"></i></span>
        <ul v-show="detailShow">
          <li v-for="part in building.parts">
            <Row class="table">
              <Col span="6">
              计划开始<p>{{ part.start_date | dateFormat}}</p></Col>
              <Col span="6">
              计划完成<p>{{ part.end_date | dateFormat}}</p></Col>
              <Col span="6">
              计划工期<p>{{ part.total_duration }}天</p></Col>
              <Col span="6">
              已经施工<p>{{ part.total_elapsed }}天</p></Col>
            </Row>
            <ul>
              <li>下面两个做成进度条</li>
              <li>计划进度: {{ part.plan_progress }}</li>
              <li>实际进度: {{ part.real_progress }}</li>
            </ul>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
  import progressbar from './progressbar/progressbar.vue'

  export default {
    props: ['db'],
    data () {
      let buildings = this.db.buildings
      return {
        buildings: buildings,
        detailShow: false
      }
    },
    methods: {
      showDetail () {
        this.detailShow = true
      },
      hideDetail () {
        this.detailShow = false
      }
    },
    components: {
      progressbar
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

  .main-table .name {
    text-align: center;
    font-size: 16px;
    font-weight: 700;
    padding: 10px 0;
  }

  .main-table .table {
    text-align: center;
    font-size: 14px;
  }

  .main-table .table p {
    font-weight: 700;
  }

/* part */
  .part .part-title {
    text-align: center;
    font-size: 16px;
  }
  .part-icon {
    display: inline-block;
    width: 100%;
    text-align: center;
    font-size: 18px;
    padding: 10px 0;
  }

</style>
