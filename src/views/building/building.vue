<template>
  <div class="building">
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
    <progressbar :real="building.real_progress" :plan="building.plan_progress"></progressbar>
    <div class="part">
      <h4 class="part-title"><i class="iconfont icon-similarproduct"></i> 分布工程</h4>
      <span class="part-icon part-unfold" v-if="!detailShow" @click="showDetail()"><i class="iconfont icon-moreunfold"></i></span>
      <span class="part-icon part-fold" v-if="detailShow" @click="hideDetail()"><i class="iconfont icon-less"></i></span>
      <transition name="slide">
        <ul v-if="detailShow">
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
            <p class="part-progress">下面两个做成进度条</p>
            <progressbar :real="part.real_progress" :plan="part.plan_progress"></progressbar>
          </li>
        </ul>
      </transition>
    </div>
  </div>
</template>

<script>
  import progressbar from '../progressbar/progressbar.vue'

  export default {
    props: {
      building: Object
    },
    data () {
      return {
        detailShow: false
      }
    },
    methods: {
      showDetail () {
        console.log('click')
        this.detailShow = true
      },
      hideDetail () {
        console.log()
        this.detailShow = false
      }
    },
    components: {
      progressbar
    }
  }
</script>

<style>
  .building .name {
    text-align: center;
    font-size: 16px;
    font-weight: 700;
    padding: 10px 0;
  }

  .building .table {
    font-size: 14px;
    margin: 5px 40px 5px;
  }

  .building .table p {
    font-weight: 700;
  }

  /* part */
  .part .part-title {
    text-align: center;
    font-weight: 700;
    font-size: 16px;
    padding-top: 5px;
  }
  .part-icon {
    display: inline-block;
    width: 100%;
    text-align: center;
    font-size: 18px;
    padding: 10px 0;
  }
  .part .part-progress {
    display: inline-block;
    width: 100%;
    font-size: 14px;
    text-align: center;
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
