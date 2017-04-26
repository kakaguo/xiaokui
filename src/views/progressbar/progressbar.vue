<template>
  <div class="progress">
    <p>实际进度</p>
    <div class="progress-num">
      <span class="planNum" :style="planwidth">{{ Math.floor(this.plan * 100) }}%</span>
      <span class="realNum" :style="realwidth">{{ Math.floor(this.real * 100) }}%</span>
    </div>
    <Progress class="real" :percent="Math.floor(real * 100)" hide-info></Progress>
    <Progress class="plan" :percent="Math.floor(plan * 100)" hide-info></Progress>
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
        return 'width:' + Math.floor(this.real * 100) + '%'
      },
      planwidth: function () {
        return 'width:' + Math.floor(this.plan * 100) + '%'
      }
    }
  }
</script>

<style>
  .progress {
    width: 100%;
    padding: 0 40px;
  }
  .progress p {
    font-size: 14px;
  }
  .progress-num {
    position: relative;
    width: 100%;
  }
  .progress-num .realNum,
  .progress-num .planNum {
    display: inline-block;
    text-align: right;
    font-size: 16px;
  }
  .progress-num .planNum {
    position: absolute;
    margin-top: 42px;
  }
  .progress-num .realNum {
    color: #2db7f5;
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
    top: -17px;
  }
</style>
