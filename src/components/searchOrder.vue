<template>
  <div>
    <div class="baseBody">
      <nav class="nav">
        <p>訂單狀態：</p>
        <div class="triangle">
          <select v-model="selected">
            <option disabled value="0">Select</option>
            <option value="1">進行中</option>
            <option value="2">已完成</option>
            <option value="3">全部顯示</option>
          </select>
        </div>
      </nav>
      <table class="bottom-line">
        <table class="table" v-if="selected == 1 || selected == 3">
          <tr>
            <th><p class="th">進行中</p></th>
          </tr>
          <div v-if="arr1">
            <tr v-for="(item, index) in arr1" :key="index">
              <Item
                class="point"
                :item="arr1[index]"
                @cancel="cancel(index, arr1[index])"
              />
            </tr>
          </div>
        </table>

        <table class="table " v-if="selected == 2 || selected == 3">
          <tr>
            <th><p class="th">已完成</p></th>
          </tr>
          <div v-if="arr2">
            <tr class="item " v-for="(item, index) in arr2" :key="index">
              <div class="circle">
                <img class="logo gray-color" :src="arr2[index].logo" alt="" />
              </div>
              <div class="content">
                <div class="tit">
                  <p>{{ arr2[index].status.type }}</p>
                </div>
                <div>{{ arr2[index].name }}</div>
              </div>
              <div>></div>
            </tr>
          </div>
        </table>
      </table>
    </div>
  </div>
</template>

<script>
import Item from "@/components/Item.vue";
export default {
  props: {
    arr1: {
      type: Array
    },
    arr2: {
      type: Array
    }
  },
  data() {
    return {
      selected: 0
    };
  },
  components: { Item },
  methods: {
    cancel(index, item) {
      item.status.code = 3;
      item.status.type = "已取消";
      this.arr1.splice(index, 1);
      this.arr2.push(item);
      console.log(localStorage.getItem("data"));
      var array = JSON.parse(localStorage.getItem("data"));
      for (var index = 0; index < array.length; index++) {
        if (array[index].name == item.name) {
          array[index] = item;
        }
      }
      console.log(array);
      console.log(typeof array);
      localStorage.setItem("data", JSON.stringify(array));
    }
  }
};
</script>

<style scoped>
.nav {
  /* background-color: cyan; */
  width: fit-content;
  display: flex;
  margin-left: 2rem;
}
/* 下拉式選單 */
select {
  position: relative;
  /*Chrome和Firefox裡面的邊框是不一樣的，所以複寫了一下*/
  border: solid 1px #000;
  /*很關鍵：將預設的select選擇框樣式清除*/
  appearance: none;
  -moz-appearance: none;
  -webkit-appearance: none;
  /*將背景改為綠色*/
  /* background: green; */
  /*留出一點位置，避免被文字覆蓋*/
  padding: 0.5rem 1rem 0.5rem 0.5rem;
  height: fit-content;
}
/*清除ie的預設選擇框樣式清除，隱藏下拉箭頭*/
/* select::-ms-expand {
  display: none;
} */
.triangle {
  position: relative;
  height: fit-content;
}
/* 小三角形 */
.triangle::after {
  position: absolute;
  left: 79%;
  top: 45%;
  content: "";
  width: 0;
  height: 0;
  border-style: solid;
  border-width: 5px 6px 0 6px;
  border-color: #000000 transparent transparent transparent;
}
.select-hide {
  display: none;
}
.table {
  width: 350px;

  /* background-color: darkorchid; */
}
.baseBody {
  display: flex;
}
/* 狀態圓圈 */
.circle {
  width: 20%;
  /* border: solid 1px; */
  border-radius: 50%;
  display: flex;
  justify-content: center;
}
.logo {
  max-width: 100%;
  width: 70%;
  object-fit: contain;
  object-position: top;
}
.item {
  display: flex;
  justify-content: space-around;
  align-items: center;
  border-color: #cdcdcd;
  border-style: solid;
  border-width: 0 1px 0 1px;
  padding: 0.7rem 0;
}
.item + .item {
  border-top: solid 1px #cdcdcd;
}

/* 狀態與時間 */
.tit {
  display: flex;
  justify-content: space-between;
  margin-bottom: 0.5rem;
}
/* 內容 */
.content {
  width: 70%;
}
th {
  /* border: solid 0.5px gray; */
  background-color: #f5f5f5;
  box-shadow: 0 0 0.7px black;
  text-align: left;
  padding: 0.5rem 0 0.5rem 1rem;
}
.th {
  border-left: solid 3px #47b134;
  padding-left: 0.3rem;
}
/* 底線工具 */
.bottom-line {
  margin-left: 2rem;
  border-bottom: solid 1px #cdcdcd;
}
.green-text {
  color: #3e9c2d;
}
.gray-color {
  filter: grayscale(100%);
}
/* 指標 */
.point {
  cursor: pointer;
}
</style>
