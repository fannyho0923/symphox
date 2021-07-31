<template>
  <div>
    <nav class="nav">
      <ul class="ul">
        <li class="togggle li" @click="togggle">訂單管理</li>
        <li v-show="isShow" class="li">訂單查詢</li>
        <li v-show="isShow" class="li">新增訂單</li>
      </ul>
    </nav>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isShow: false
    };
  },
  methods: {
    togggle() {
      if (this.isShow) {
        this.isShow = false;
      } else {
        this.isShow = true;
      }
    }
  }
};
</script>

<style scoped>
/* 表單外框 */
.nav {
  display: inline-block;
  margin: 1.5rem 0 0 2.5rem;
  border: solid 1px;
}
.ul {
  margin: 0.5rem 3rem 1.5rem 1rem;
}
li + li {
  margin-top: 1rem;
}
/* 項目 */
.li {
  cursor: pointer;
}
.togggle::before {
  position: absolute;
  left: -16%;
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
</style>
