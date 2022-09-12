<template>
  <div class="container">
    <div class="firstBox">
      <!-- 第一层 -->
      <div v-if="!treeDataSc.length">
        <div
          class="first"
          v-for="(item, index) in treeData"
          :key="index"
          @click="chooseClick(index)"
        >
          {{ item.title }}
        </div>
      </div>
      <!-- 第二层 -->
      <div v-else-if="treeDataSc.length">
        <div
          class="second"
          v-for="(item, index) in treeDataSc"
          :key="index"
          @click="chooseClickSc(index)"
        >
          {{ item.title }}
        </div>
      </div>
    </div>
    <div class="secondBox">
      <!-- 第三层 -->
      <div v-if="treeDataTh.length && !treeDataFr.length && !treeDataFif.length">
        <div
          class="third"
          v-for="(item, index) in treeDataTh"
          :key="index"
          @click="chooseClickTh(index)"
        >
          {{ item.title }}
        </div>
      </div>
      <!-- 第四层 -->
      <div v-else-if="treeDataFr.length && !treeDataFif.length">
        <div
          class="forth"
          v-for="(item, index) in treeDataFr"
          :key="index"
          @click="chooseClickFr(index)"
        >
          {{ item.title }}
        </div>
      </div>
      <!-- 第五层 -->
      <div v-else-if="treeDataFif.length">
        <div class="fifth" v-for="(item, index) in treeDataFif" :key="index">
          {{ item.title }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      treeData: [
        {
          title: "第一层a",
          index: 1,
          children: [
            {
              title: "第二层a",
              index: 1,
              children: [
                {
                  title: "第三层a",
                  index: 1,
                  children: [
                    {
                      title: "第四层a",
                      index: 1,
                      children: [
                        {
                          title: "第五层a",
                          index: 1,
                        },
                      ],
                    },
                  ],
                },
              ],
            },
          ],
        },
        {
          title: "第一层b",
          index: 1,
          children: [
            {
              title: "第二层b",
              index: 1,
              children: [
                {
                  title: "第三层b",
                  index: 1,
                  children: [
                    {
                      title: "第五层b",
                      index: 1,
                    },
                  ],
                },
              ],
            },
          ],
        },
        {
          title: "第一层c",
          index: 1,
          children: [
            {
              title: "第二层c",
              index: 1,
              children: [
                {
                  title: "第五层c",
                  index: 1,
                },
              ],
            },
          ],
        },
        {
          title: "第一层d",
          index: 1,
          children: [
            {
              title: "第五层c",
              index: 1,
            },
          ],
        },
      ],
      treeDataSc: [],
      treeDataTh: [],
      treeDataFr: [],
      treeDataFif: [],
    };
  },
  mounted() {},
  methods: {
    chooseClick(val) {
      let flag = false;
      this.treeData[val].children.filter((item) => {
        return (flag = item.children);
      });
      if (flag) {
        this.treeDataSc = this.treeData[val].children;
      } else {
        this.treeDataFif = this.treeData[val].children;
      }
    },
    chooseClickSc(val) {
      let flag = false;
      this.treeDataSc[val].children.filter((item) => {
        return (flag = item.children);
      });
      if (flag) {
        this.treeDataTh = this.treeDataSc[val].children;
      } else {
        this.treeDataFif = this.treeDataSc[val].children;
      }
    },
    chooseClickTh(val) {
      let flag = false;
      this.treeDataTh[val].children.filter((item) => {
        return (flag = item.children);
      });
      if (flag) {
        this.treeDataFr = this.treeDataTh[val].children;
      } else {
        this.treeDataFif = this.treeDataTh[val].children;
      }
    },
    chooseClickFr(val) {
      this.treeDataFif = this.treeDataFr[val].children;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

.container {
  display: block;
  width: 1200px;
  height: 100vh;
  margin: 0 auto;
}
.firstBox {
  width: 100%;
  background-color: #fff;
}
.first,
.second,
.third,
.forth,
.fifth {
  display: inline-block;
  width: 290px;
  height: 200px;
  margin-right: 10px;
  background-color: red;
}
.second{
  background-color: green;
}
.third{
  background-color: pink;
}
.forth{
  background-color: skyblue;
}
.fifth{
  background-color: blue;
}

</style>
