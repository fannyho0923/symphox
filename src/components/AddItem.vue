<template>
  <div>
    <nav class="nav">
      <div class="nameBox">
        <label>商品名稱：</label>
        <input v-model="name" type="text" required @change="edit(1)" />
      </div>
      <div class="logoBox">
        <label>圖示連結：</label>
        <input v-model="logo" type="text" required @change="edit(2)" />
      </div>
      <div class="statusBox">
        <label>訂單狀態：</label>
        <div class="triangle">
          <select class="select" v-model="selected" required @change="edit(3)">
            <option disabled value="0">Select</option>
            <option value="1">進行中</option>
            <option value="2">已完成</option>
            <option value="3">全部顯示</option>
          </select>
        </div>
      </div>
    </nav>
  </div>
</template>

<script>
export default {
  props: {
    i: {
      type: Number
    }
  },
  data() {
    return {
      selected: 0,
      name: "",
      logo: ""
    };
  },
  methods: {
    edit(j) {
      if (j == 1) {
        this.$emit("edit", this.i, this.name, j);
      }
      if (j == 2) {
        this.$emit("edit", this.i, this.logo, j);
      }
      if (j == 3) {
        if (this.selected) {
          this.$emit("edit", this.i, this.selected, j);
        }
      }
    }
  }
};
</script>

<style scoped>
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
/* 新物品名稱容器 */
.nameBox {
  margin-bottom: 0.5rem;
}
/* 新物品照片容器 */
.logoBox {
  margin-bottom: 0.5rem;
}
/* 新物品狀態容器 */
.statusBox {
  display: flex;
}
.nav {
  margin-bottom: 1rem;
  margin-right: 1rem;
  /* background-color: teal; */
}

.select {
  width: 100%;
}
</style>
