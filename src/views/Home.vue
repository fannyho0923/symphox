<template>
  <div>
    <div class="container">
      <nav class="nav">
        <ul class="ul">
          <li class="togggle li" @click="togggle">訂單管理</li>
          <li v-show="isShow" class="li" @click="searchOrder">訂單查詢</li>
          <li v-show="isShow" class="li" @click="addOrder">新增訂單</li>
        </ul>
      </nav>
      <div v-if="showSearch" class="selectBox">
        <SearchOrder :arr1="arr1" :arr2="arr2" />
      </div>
      <div v-if="showAdd" class="selectBox">
        <AddOrder />
      </div>
    </div>
  </div>
</template>

<script>
import SearchOrder from "@/components/searchOrder";
import AddOrder from "@/components/AddOrder";
export default {
  data() {
    return {
      isShow: false,
      showSearch: false,
      showAdd: false,
      data: null,
      arr1: [],
      arr2: []
    };
  },
  components: {
    SearchOrder,
    AddOrder
  },
  watch: {
    isShow() {
      if (!this.isShow) {
        this.showSearch = false;
      }
    }
  },
  created() {
    this.axios.get("../../static/data.json").then(response => {
      //   this.listData = response.data;
      this.data = response.data;

      localStorage.setItem("data", JSON.stringify(this.data));
      console.log(response.data);
      for (var index = 0; index < this.data.length; index++) {
        if (
          this.data[index].status.code > 0 &&
          this.data[index].status.code < 3
        ) {
          this.arr1.push(this.data[index]);
        } else {
          this.arr2.push(this.data[index]);
        }
      }
    });
  },
  methods: {
    // 展開功能
    togggle() {
      if (this.isShow) {
        this.isShow = false;
      } else {
        this.isShow = true;
      }
    },
    // 查看訂單
    searchOrder() {
      if (this.isShow) {
        this.showAdd = false;
        this.showSearch = true;
      }
    },
    // 新增訂單
    addOrder() {
      if (this.isShow) {
        this.showSearch = false;
        this.showAdd = true;
      }
    }
  }
};
</script>

<style scoped>
/* 表單外框 */
.nav {
  height: fit-content;
  display: inline-block;
  margin: 1.5rem 0 0 2.5rem;
  border: solid 1px;
  padding-bottom: 1rem;
  padding-left: 0.5rem;
}
.ul {
  margin: 0 0 0 1rem;
}
li + li {
  /* margin-top: 1rem; */
}
/* 項目 */
.li {
  /* background-color: cornflowerblue; */
  cursor: pointer;
  padding: 0.5rem 3rem 0.5rem 0;
}
.togggle::before {
  position: absolute;
  left: -12%;
  top: 50%;
  content: "";
  width: 0;
  height: 0;
  border-style: solid;
  border-width: 5px 4px 0 4px;
  border-color: #000000 transparent transparent transparent;
}
.togggle {
  position: relative;
}
.container {
  display: flex;
}
.selectBox {
  margin-top: 1.5rem;
}
</style>
