<template>
  <div class="tower-item">
    <div class="tower-head">
      <div class="tower-title">Уровень карналита в&nbsp;силосной башне&nbsp;{{getTowerNum(params.title)}}</div>
      <div class="tower-value-percents">
        <div class="tower-value-percents-num">{{ getTowerPer(params.maxValue, params.value) }}%</div>
        <div class="tower-value-percents-progress" :class="{ 'low-level' : params.value < params.minValue, 'high-level' : params.value > params.maxValue}">
          <div class="progress-val" :style="{ width: getTowerPer(params.maxValue, params.value)+'%' }"></div>
        </div>
      </div>
    </div>
    <div class="tower-body">
      <div class="tower-borders"><span></span><span></span></div>
      <div class="tower-body-value" :style="{ height: getTowerPer(params.maxValue, params.value)+'%' }"></div>
    </div>
    <div class="tower-body-footer">
      <div class="tower-body-footer-bck"></div>
    </div>
    <div class="tower-footer">
      <div class="tower-footer-title">Масса карналита</div>
      <div class="tower-value-percents-num">{{ numberWithCommas(params.value)}}</div>
      <div class="tower-value-percents-progress" :class="{ 'low-level' : params.value < params.minValue, 'high-level' : params.value > params.maxValue}">
        <div class="progress-val" :style="{ width: getTowerPer(params.maxValue, params.value)+'%' }"></div>
      </div>
    </div>

    <input type="range" v-model="params.value"  min="0" :max="params.maxValue+100" @change.prevent="$emit('update')" />

  </div>
</template>

<script>
export default {
  name: 'TowerItem',
  props: {
    params: {
      type: Object
    },
  },
  data () {
    return {}
  },
  methods: {
    getTowerNum (title){
      var towerNum = title.split(' ')
      return (towerNum[1])
    },
    getTowerPer (v_max, v_val){
      var curPer = ( v_val/v_max * 100)
      return parseInt(curPer)
    },
    numberWithCommas(x) {
      return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, " ");
    }
  }
}
</script>

<style scoped>
  .tower-item{
    position: relative;
    padding: 0 15px;
    max-width: 170px;
    margin-bottom: 60px;
    text-align: center;
  }
  .tower-title{
    display: flex;
    justify-content: center;
    align-items: flex-end;
    min-height: 70px;
    margin-bottom: 5px;
  }
  .tower-value-percents-progress{
    position: relative;
    width: 100%;
    max-width: 60px;
    margin: 5px auto;
    height: 3px;
  }
  .progress-val{
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    top: 0;
    height: 100%;
    background-color: #21b149;
  }
  .low-level .progress-val,
  .high-level .progress-val{background-color: #c35b5b;}
  .tower-value-percents-num{font-size: 26px;}
  .tower-body{
    position: relative;
    margin: 40px auto 8px;
    max-width: 130px;
    background: rgb(97,97,102);
    background: linear-gradient(90deg, rgba(97,97,102,1) 0%, rgba(154,154,154,1) 25%, rgba(97,97,102,1) 100%);
    height: 340px;
  }
  .tower-body-footer{position: relative;max-width: 130px;margin: 0 auto;}
  .tower-body-footer-bck{
    position: relative;
    background: rgb(97,97,102);
    background: linear-gradient(90deg, rgba(97,97,102,1) 0%, rgba(154,154,154,1) 25%, rgba(97,97,102,1) 100%);
    height: 65px;
    clip-path: polygon(0 0, 100% 0, 58% 100%, 42% 100%);
  }
  .tower-body-footer:before{
    content: '';
    position: absolute;
    left: 10px;
    top: 10px;
    width: 55px;
    height: 35px;
    border-radius: 5px;
    border: 4px solid #21b149;
    z-index: 5;
  }
  .tower-body:before{
    content: '';
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    height: 4px;
    width: 50px;
    background-color: #8b959f;
    top: -15px;
  }
  .tower-body-value{
    position: absolute;
    left: 10px;
    right: 10px;
    bottom: 0;
    background-color: #21b249;
    opacity: .5;
    max-height: 100%;
    transition: height .25s cubic-bezier(1,.51,.46,1);
    z-index: 10;
  }
  .tower-borders{
    position: absolute;
    left: -10px;
    top: -10px;
    right: -10px;
    bottom: -5px;
    z-index: 5;
  }
  .tower-borders:after,
  .tower-borders span:before,
  .tower-borders span:after{
    content: '';
    position: absolute;
    left: -2px;
    right: -2px;
    height: 4px;
    border: 2px solid #2d2d32;
    background-color: #cbcbcb;
    transform: translateY(-50%);
  }
  .tower-borders span:before{transform: none;top: 1px;}
  .tower-borders span:after{top: 25%;}
  .tower-borders span+span:before{top: 50%;}
  .tower-borders span+span:after{top: 75%;}
  .tower-borders:after{top: 100%;margin-top: -1px;}
  .tower-footer{margin-top: 30px;margin-bottom: 15px;}
  .tower-footer-title{margin-bottom: 5px;}

  @media (max-width: 510px) {
    .tower-item{font-size: 12px;max-width: 150px;}
  }

</style>
