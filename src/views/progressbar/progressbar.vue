<template>
  <div class="progress">
    <p>实际进度</p>
    <div>
      <span class="realNum" :style="realwidth"></span><span>real</span>
      <span class="planNum" :style="planwidth"></span><span>plan</span>
    </div>
    <Progress class="real" :percent="Math.floor(real * 100)"></Progress>
    <Progress class="plan" :percent="Math.floor(plan * 100)"></Progress>
    <p>计划进度</p>
  </div>
</template>

<script>
  /* eslint-disable no-unused-vars */
  import iView from 'iview'
  import 'iview/dist/styles/iview.css'

  export default {
    props: {
      real: {
        type: Number
      },
      plan: {
        type: Number
      }
    },
    computed: {
      realwidth: function () {
        return 'width:' + this.real * 100 + '%'
      },
      planwidth: function () {
        return this.plan * 100 + '%'
      }
    }
  }
</script>

<style>
  .progress {
    width: 100%;
  }
  .progress .realNum {
    display: inline-block;
    border: 1px solid red;
  }
  .ivu-progress-bg {
    height: 15px !important;
  }

  .plan .ivu-progress-inner {
    background: none;
  }

  .plan .ivu-progress-text {
    position: absolute;
    top: -1px;
    border: 1px solid red;
  }

  .plan {
    top: -1px;
  }
</style>
