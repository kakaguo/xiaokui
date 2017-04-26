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
      </ul>
      <div class="part">
        <h4 class="part-title"><i class="iconfont icon-similarproduct"></i> 分布工程</h4>
        <span class="part-icon part-unfold" v-if="!building.detailShow" @click="showDetail(building)"><i class="iconfont icon-moreunfold"></i></span>
        <span class="part-icon part-fold" v-if="building.detailShow" @click="hideDetail(building)"><i class="iconfont icon-less"></i></span>
        <transition name="slide">
          <ul v-if="building.detailShow">
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
                <progressbar :real="part.real_progress" :plan="part.plan_progress"></progressbar>
              </ul>
            </li>
          </ul>
        </transition>
      </div>
    </div>
  </div>
</template>

<script>
  import Vue from 'Vue'
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
      showDetail (building) {
        Vue.set(building, building.detailShow, true)
        building.detailShow = true
      },
      hideDetail (building) {
        Vue.set(building, building.detailShow, false)
        building.detailShow = false
      }
    },
    created () {
      for (let key in this.buildings) {
        this.buildings[key].detailShow = false
      }
      console.log('1', this.buildings)
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
    font-size: 14px;
    margin: 0 40px 15px;
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
  .part .ivu-progress-bg {
    height: 10px !important;
  }

  .slide-enter-active, .slide-leave-active {
    transition: all .8s;
  }
  .slide-enter, .slide-leave-active {
    transform: translateY(-50px);
    opacity: 0;
  }

</style>
