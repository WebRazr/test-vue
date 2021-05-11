<template>
  <div>
    <button class="btn" v-on:click="loadDataFunc">Get data</button>
    <div v-if="transformData === null && loader === false">
      <p :style="'font-size: 2em'">no data</p>
    </div>

    <div id="t-block" v-else>
      <div v-if="loader"><Loader /></div>
      <div v-else id="table">
        <div class="line-block title-color">
          <div
            class="center-data-block"
            v-for="(item, index) in titleArr"
            :key="index + item"
          >
            <p>{{ item }}</p>
          </div>
        </div>
        <div
          class="line-block other-color"
          v-for="(item, index) in transformData"
          :key="index"
        >
          <Stocks :stock="item.st" />
          <Start :start="item.startData" />
          <Current :total="item.сurrentData" />
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import Stocks from "./tableComponent/Stocks";
import Current from "./tableComponent/Current";
import Start from "./tableComponent/Start";
import getDataFunc from "./../../plugins/getDataFunc";
import Loader from "./../loader/loader";
import { payload } from "./../../mocData/index";
export default {
  name: "MainTable",
  components: {
    Loader,
    Stocks,
    Current,
    Start,
  },
  data() {
    return {
      newData: null,
      loader: false,
      transformData: null,
      titleArr: ["Stocks", "Start", "Current"],
    };
  },
  methods: {
    async startMethod() {
      try {
        const data = await getDataFunc(payload);

        this.newData = data;
        const { stocks, start, current } = data;
        this.transformData = null;
        const newObj = (i, b) => {
          return {
            st: stocks[i],
            startData: start[i],
            сurrentData: { value: current[i].toFixed(2), cur: b },
          };
        };
        const dataTransform = start.map((startValue, index) => {
          if (current[index] > startValue) {
            return newObj(index, true);
          } else {
            return newObj(index, false);
          }
        });
        const sortArr = dataTransform.sort((a, b) => {
          let nameA = a.st.toLowerCase(),
            nameB = b.st.toLowerCase();
          if (nameA < nameB) return -1;
          if (nameA > nameB) return 1;
          return 0;
        });
        this.transformData = sortArr;
        this.loader = false;
      } catch (err) {
        this.transformData = null;
        this.loader = false;
      }
    },
    loadDataFunc() {
      this.loader = true;
      this.startMethod();
    },
  },
};
</script>

<style lang="scss">
#t-block {
  display: flex;

  flex-direction: column;
  align-items: center;
  justify-content: center;
}
#table {
  margin-top: 20px;
  width: 500px;
}
.title-color {
  border-radius: 4px 4px 0 0;
  background: #f2f2f2;
  div {
    p {
      font-size: 2em;
      font-weight: 600;
    }
  }
}
.other-color {
  background: #fff;
}
.line-block {
  display: flex;
  justify-content: space-between;
  border: 1px solid black;
}
.center-data-block {
  width: calc(100% / 3);
  display: flex;
  justify-content: center;
}
.btn {
  width: 150px;
  height: 50px;
  border-radius: 15px;
  font-size: 1.2em;
}
p {
  font-size: 1.5em;
}
</style>
