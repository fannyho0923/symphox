<template>
  <div>
    <div class="itemBox">
      <AddItem />
      <div class="addBtn">+</div>
    </div>
    <div class="sendBtn" @click="addAllItem">新增</div>
  </div>
</template>

<script>
import AddItem from "@/components/AddItem.vue";
export default {
  components: {
    AddItem
  },
  methods: {
    addAllItem() {}
  }
};
</script>

<style scoped>
/* 輸入多筆訂單 */
.addBtn {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 35px;
  height: 35px;
  background-color: #116bc8;
  border-radius: 50%;
  color: white;
  font-size: 3rem;
  margin-left: 2rem;
  margin-top: 0.5rem;
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
</style>
