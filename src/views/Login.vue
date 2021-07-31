<template>
  <div>
    <!-- 表單容器 -->
    <form class="form">
      <header class="header"><h1 class="title">登入</h1></header>
      <!-- 輸入框容器 -->
      <div class="inputBox">
        <!-- 帳號輸入 -->
        <input
          type="email"
          v-model="userName"
          placeholder="輸入帳號"
          autocomplete="off"
          required
        />
        <!-- 密碼輸入 -->
        <input
          type="password"
          v-model="password"
          placeholder="輸入密碼"
          autocomplete="off"
          oninput="value=value.replace(/[^\d]/g,'')"
          required
        />
        <div>
          <!-- 登入按鈕 -->
          <button class="btn" @click.prevent="login">Login</button>
        </div>
      </div>
    </form>
  </div>
</template>
<script>
export default {
  data() {
    return {
      userName: "",
      password: "",
      userNameAns: "fannyho0923@gmail.com",
      passwordAns: 12345,
      auth: false
    };
  },
  methods: {
    // 驗證帳密

    login() {
      if (
        this.userName == this.userNameAns &&
        this.password == this.passwordAns
      ) {
        this.auth = true;
      }

      if (this.auth) {
        this.$router.push("/home");
      } else {
        alert("login failed");
      }
    }
  }
};
</script>
<style scoped>
/* 表單 */
.form {
  margin: 8rem auto;
  width: 300px;
  border: solid 1px;
  border-radius: 5px;
  padding-bottom: 1rem;
}

/* 登入按鈕 */
.btn {
  color: rgb(211, 210, 210);
  background-color: #424242;
  width: fit-content;
  float: right;
  padding: 0.3rem 1rem;
}
.btn:hover {
  cursor: pointer;
}
/* 標題 */
.header {
  background-color: #eee;
  border-radius: 5px 5px 0 0;
}
.title {
  padding: 0.4rem;
}
/* 輸入框容器 */
.inputBox {
  margin: 1.3rem auto;
  display: flex;
  flex-direction: column;
  width: 70%;
}
input {
  padding: 0.3rem 0.2rem;
  margin-bottom: 1rem;
}
</style>
