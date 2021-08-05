<template>
  <div>
    <div class="itemBox">
      <div class="scrollBox">
        <div v-for="(item, index) in count" :key="index">
          <AddItem :count="count" :i="index" @edit="edit" />
        </div>
      </div>
      <div class="addBtn" @click="addItem"><span class="span">+</span></div>
    </div>
    <div class="sendBtn" @click="addAllItem">新增</div>
  </div>
</template>

<script>
import AddItem from "@/components/AddItem.vue";
export default {
  data() {
    return {
      count: 0,
      arr: [],
      date: new Date()
    };
  },
  components: {
    AddItem
  },
  methods: {
    addItem() {
      this.count++;
    },
    addAllItem() {
      var ans = [];
      var i = 0;
      if (this.arr) {
        for (var index = 0; index < this.arr.length; index++) {
          if (
            this.arr[index].name &&
            this.arr[index].logo &&
            this.arr[index].status
          ) {
            ans.push(this.arr[index]);
            i++;
          }
        }
        if (i > 0) {
          alert("成功新增 " + i + " 個商品");
        }
        // console.log(this.arr);
        this.arr = [];
        this.count = 0;

        //   console.log(localStorage.getItem("data"));
        var array = JSON.parse(localStorage.getItem("data"));
        for (var index = 0; index < ans.length; index++) {
          array.push(ans[index]);
        }
        //   console.log(typeof array);
        localStorage.setItem("data", JSON.stringify(array));
        console.log(localStorage.getItem("data"));

        return;
      }
    },

    edit(index, data, i) {
      if (index < this.arr.length) {
        if (i === 1) {
          this.arr[index].name = data;
        }
        if (i === 2) {
          this.arr[index].logo = data;
        }
        if (i === 3) {
          var statuses = {};
          data = Number(data);
          switch (data) {
            case 1:
              statuses.code = data;
              statuses.type = "處理中";
              break;
            case 2:
              statuses.code = data;
              statuses.type = "已成立";
              break;
            case 3:
              statuses.code = data;
              statuses.type = "已取消";
              break;
          }
          this.arr[index].status = statuses;
        }
        this.arr[index].date = `${this.date.getFullYear() -
          1911}/${this.date.getMonth() + 1}/${this.date.getDay() + 1}`;
      }
      if (index >= this.arr.length) {
        var ans = {};
        if (i === 1) {
          ans.name = data;
        }
        if (i === 2) {
          ans.logo = data;
        }
        if (i === 3) {
          var statuses = [];
          data = Number(data);
          switch (data) {
            case 1:
              statuses.code = data;
              statuses.type = "處理中";
              break;
            case 2:
              statuses.code = data;
              statuses.type = "已成立";
              break;
            case 3:
              statuses.code = data;
              statuses.type = "已取消";
              break;
          }
          ans.status = statuses;
        }
        ans.date = `${this.date.getFullYear() - 1911}/${this.date.getMonth() +
          1}/${this.date.getDay() + 1}`;
        this.arr.push(ans);
      }
    }
  }
};
</script>

<style scoped>
/* 輸入多筆訂單 */
.addBtn {
  position: relative;
  width: 35px;
  height: 35px;
  background-color: #116bc8;
  border-radius: 50%;
  color: white;
  margin-left: 2rem;
  margin-top: 0.5rem;
  cursor: pointer;
}
.span {
  cursor: pointer;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -59%);
  font-size: 3rem;
}
.itemBox {
  margin-left: 2rem;
  display: flex;
}
/* 新增所有item */
.sendBtn {
  cursor: pointer;
  position: fixed;
  border: solid 1px;
  padding: 0.5rem 2rem;
  right: 10%;
  top: 80%;
}
.scrollBox {
  overflow-y: auto;
  height: 35rem;
}
/* 捲軸底色 */
.scrollBox::-webkit-scrollbar-track {
  -webkit-box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.3);
  /* background-color: #95b3f8; */
}
/* 捲軸寬度 */
.scrollBox::-webkit-scrollbar {
  width: 6px;
  /* background-color: black; */
}
/* 捲軸本體顏色 */
.scrollBox::-webkit-scrollbar-thumb {
  /* background-color: #3f76f7; */
}
</style>
