<template>
  <div class="baseBody">
    <div class="box">
      <label>要取消訂單? </label>
      <div class="btnBox">
        <div class="btn" @click.prevent="yes">確定</div>
        <div class="btn" @click.prevent="no">再想想</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    yes() {
      this.$emit("cancel", true);
    },
    no() {
      this.$emit("cancel", false);
    }
  }
};
</script>

<style scoped>
.box {
  border: solid 1px;

  width: 150px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding-top: 0.5rem;
}
/* 按鈕容器 */
.btnBox {
  width: 100%;
  display: flex;
  justify-content: space-evenly;
}
.btn {
  margin: 0.5rem 0;
  padding: 0.2rem 0;
  border: solid 1px;
}
.btn:hover {
  background-color: rgb(252, 252, 122);
}
</style>
