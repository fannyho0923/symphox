<template>
  <div class="base__body">
    <div class="circle">
      <img class="logo" :src="item.logo" alt="" />
    </div>
    <div class="content">
      <div class="tit">
        <p class="green-text">{{ item.status.type }}</p>
        <p>預計出貨：{{ item.date }}</p>
      </div>
      <div>{{ item.name }}</div>
    </div>
    <div class="choosedBtn" @click.prevent="choosed">></div>
    <CancelPop v-if="isShow" class="cancelBox" @cancel="cancel" />
  </div>
</template>

<script>
import CancelPop from "@/components/CancelPop.vue";
export default {
  props: { item: { type: Object } },
  components: { CancelPop },
  data() {
    return {
      isShow: false
    };
  },
  methods: {
    choosed() {
      if (this.isShow) {
        this.isShow = false;
      } else {
        this.isShow = true;
      }
    },
    cancel(data) {
      if (data) {
        this.isShow = false;
        this.$emit("cancel");
      } else {
        this.isShow = false;
      }
      console.log(this.isShow);
    }
  }
};
</script>

<style scoped>
.base__body {
  position: relative;
  display: flex;
  justify-content: space-around;
  align-items: center;
  border-color: #cdcdcd;
  border-style: solid;
  border-width: 1px 1px 0 1px;
  padding: 0.7rem 0;
}
/* 內容 */
.content {
  width: 70%;
}
/* 狀態與時間 */
.tit {
  display: flex;
  justify-content: space-between;
  margin-bottom: 0.5rem;
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
/* 底線工具 */
.bottom-line {
  border-bottom: solid 1px #cdcdcd;
}
.green-text {
  color: #3e9c2d;
}
.cancelBox {
  position: absolute;
  left: 101%;
  top: 12%;
}
.choosedBtn {
  height: 100%;
}
</style>
