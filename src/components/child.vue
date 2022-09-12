<template>
    <div  v-for="(item,ind) in dataObj" :key="item.index" @click.stop="showChildrenFn(item)">
      <div v-if="item.children && item.children.length> 0" :style="{backgroundColor: coloring()}" class="children-class">
        <h1 style="z-index: 999;">{{item.title}}</h1>
        <child :dataObj="item.children"  v-if="item.children[0].title === showChildren"></child>
      </div>
      <div v-else :style="{backgroundColor: coloring()}" class="children-class">
        <h1 style="z-index: 999;">{{item.title}}</h1>
      </div>
    </div >
</template>

<script lang="ts" setup>
import { onMounted } from 'vue';
import { ref } from 'vue'
  interface IProps {
    title?: string,
    index?:number,
    children?: Array<IProps>
  }
  const showChildren = ref<string>('')
  const showChildrenFn = (item:any) => {
    if(item.children&&item.children[0]) {
      showChildren.value = item.children[0].title
    }
  }
  defineProps<{ dataObj: IProps[]}>();
  const  coloring = () => {
    let r = Math.floor(Math.random() * 255)
    let g = Math.floor(Math.random() * 255)
    let b = Math.floor(Math.random() * 255)
    return `rgb(${r}, ${g}, ${b})`
}

</script>

<style lang="scss" scoped>
  div {
    width: 200px;
    height:200px;
    background-color: green;
    margin-right: 20px;
  }
  .children-class {
    // position: absolute;
    top: 200px;
    display: flex;
    flex-direction: column;
  }
  .child-container {
    display: flex;
    margin-right: 100px;
    flex-direction: column;
  }
</style>
