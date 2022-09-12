<template>
  <div class="container">
    <div :class="`container-item`"  v-for="item in data" :key="item.title" @click.stop="showChildrenFn(item)">
      <h1>{{item.title}}</h1>
      <!-- <div :style="{backgroundColor: coloring()}" style="margin-top:300px;" v-for="i in item.children" :key="i.index"></div> -->
    </div>
  </div>
  <div class="child-container">
    <template  v-for="item in data" :key="item.title" @click.stop="showChildrenFn(item)">
      <child :dataObj="item.children"  v-if="item.title === showChildren"/>
    </template>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue'
import { data } from './components/index'
import child from './components/child.vue'

const showChildren = ref<string>('')
  const showChildrenFn = (item:any) => {
    showChildren.value = item.title
  }
</script>

<style lang="scss" scoped>
.container {
  background-color: pink;
  display: flex;
  .container-item {
    position: relative;
    width:200px;
    height: 200px;
    margin-right: 100px;
    background-color: green;
  }
}
</style>
