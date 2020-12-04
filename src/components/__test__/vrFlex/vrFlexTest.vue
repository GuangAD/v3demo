<template>
  <vr-flex style="width: 350px;height: 600px" class="test-flex"
  :direction='direction'
  :wrap='wrap'
  :justify-content='justifyContent'
  :align-items='alignItems'
  :align-content='alignContent'
  :average='average'
  :gap='gap'
  :row-gap='rowGap'
  :column-gap='columnGap'
  :wrap-gap='wrapGap'>
    <div class="clild">1</div>
    <div class="clild">2</div>
    <div class="clild">3</div>
    <div class="clild">4</div>
    <div class="clild">5</div>
    <div class="clild">6</div>
    <div class="clild">7</div>
    <div class="clild">8</div>
    <div class="clild">9</div>
  </vr-flex>
  <div>
    <span>direction：主轴方向</span>
    <input type="radio" value="row" v-model="direction"/>
    <label for="">row</label>
    <input type="radio" value="column" v-model="direction"/>
    <label for="">column</label>
  </div>
  <div>
    <span>wrap：主轴方向</span>
    <input type="radio" :value="true" v-model="wrap"/>
    <label for="">true</label>
    <input type="radio" :value="false" v-model="wrap"/>
    <label for="">false</label>
  </div>
  <div>
    <span>justifyContent：主轴对齐</span>
    <input type="radio" value="start" v-model="justifyContent"/>
    <label for="">start</label>
    <input type="radio" value="end" v-model="justifyContent"/>
    <label for="">end</label>
    <input type="radio" value="center" v-model="justifyContent"/>
    <label for="">center</label>
    <input type="radio" value="around" v-model="justifyContent"/>
    <label for="">around</label>
    <input type="radio" value="between" v-model="justifyContent"/>
    <label for="">between</label>
  </div>
  <div>
    <span>alignItems：副轴单轴</span>
    <input type="radio" value="start" v-model="alignItems"/>
    <label for="">start</label>
    <input type="radio" value="end" v-model="alignItems"/>
    <label for="">end</label>
    <input type="radio" value="center" v-model="alignItems"/>
    <label for="">center</label>
    <input type="radio" value="baseline" v-model="alignItems"/>
    <label for="">baseline</label>
    <input type="radio" value="stretch" v-model="alignItems"/>
    <label for="">stretch</label>
  </div>
  <div>
    <span>alignContent：副轴对齐</span>
    <input type="radio" value="start" v-model="alignContent"/>
    <label for="">start</label>
    <input type="radio" value="end" v-model="alignContent"/>
    <label for="">end</label>
    <input type="radio" value="center" v-model="alignContent"/>
    <label for="">center</label>
    <input type="radio" value="around" v-model="alignContent"/>
    <label for="">around</label>
    <input type="radio" value="between" v-model="alignContent"/>
    <label for="">between</label>
    <input type="radio" value="stretch" v-model="alignContent"/>
    <label for="">stretch</label>
  </div>
  <div>
    <span>average：row平分</span>
    <input type="radio" :value="true" v-model="average"/>
    <label for="">true</label>
    <input type="radio" :value="false" v-model="average"/>
    <label for="">false</label>
  </div>
  <div>
    <span>gap</span>
    <input type="text" v-model.number="gap">
    <span>{{gap}}</span>
  </div>
  <div>
    <span>rowGap</span>
    <input type="text" v-model.number="rowGap">
    <span>{{rowGap}}</span>
  </div>
  <div>
    <span>columnGap</span>
    <input type="text" v-model.number="columnGap">
    <span>{{columnGap}}</span>
  </div>
  <div>
    <span>wrapGap</span>
    <input type="text" v-model.number="wrapGap">
  </div>
</template>

<script lang='ts'>
import { defineComponent, ref } from 'vue'
import VrFlex from '../../flex/vrFlex.vue'
export default defineComponent({
  name: 'VrFlexTest',
  components: {
    VrFlex
  },
  setup () {
    const direction = ref('row')
    const wrap = ref(true)
    const justifyContent = ref('start')
    const alignItems = ref('start')
    const alignContent = ref('start')
    const average = ref(false)
    const gap = ref(10)
    const rowGap = ref(10)
    const columnGap = ref(10)
    const wrapGap = ref(0)
    return {
      direction,
      wrap,
      justifyContent,
      alignItems,
      alignContent,
      average,
      gap,
      rowGap,
      columnGap,
      wrapGap
    }
  }
})
</script>

<style>
.clild{
  /* width: 100px; */
  /* height: 100px; */
  line-height: 100px;
  text-align: center;
  font-size: 26px;
  background-color: blue;
  color: #fff;
}
.test-flex{
  border: 1px solid #000;
}
</style>