<template>
  <div>
    <nav class="nav">
      <ul class="ul">
        <li class="li">訂單管理</li>
        <li class="li">訂單查詢</li>
        <li class="li">新增訂單</li>
      </ul>
    </nav>
  </div>
</template>

<script>
export default {};
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
</style>
