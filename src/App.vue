<template>
  <div class="contanier">
    <div class="menu">
      <div v-for="(value, name) in allComponent" :key="name"
      @click="changeActiveKey(name)"
      >{{name}}</div>
    </div>
    <div class="content">
      <component :is='allComponent[activeKey]'></component>
    </div>
  </div>
</template>

<script lang='ts'>
import { defineComponent, reactive, ref } from 'vue'
import VrFlex from './components/__test__/vrFlex/vrFlexTest.vue'
export default defineComponent({
  name: 'App',
  setup(){
    const allComponent = reactive({
      vrFlex: VrFlex
    })
    const activeKey = ref('vrFlex')
    function changeActiveKey (name: string) {
      activeKey.value = name
    }
    return {
      allComponent,
      activeKey,
      changeActiveKey
    }
  }
})
</script>

<style scoped>
.contanier{
  box-sizing: border-box;
  width: 100vw;
  height: 100vh;
  padding: 20px;
  display: flex;
}
.menu{
  width: 80px;
  background-color: red;
}
.menu > * {
  height: 50px;
  line-height: 50px;
  text-align: center;
}
.content{
  flex-grow: 1;
  padding: 20px;
  border: 1px solid #333;
  overflow: scroll;
}
</style>