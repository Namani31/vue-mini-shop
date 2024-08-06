<template>
  <div class="container mt-5">
    <div class="row justify-content-center">
      <div class="col-md-6">
        <div class="card">
          <div class="card-header">로그인</div>
          <div class="card-body">
            <form action="">
              <div class="form-group d-flex align-items-center">
                <label for="user-name" class="mr-2">사용자 이름:</label>
                <input
                  type="text"
                  class="form-control flex-grow-1"
                  id="username"
                  v-model="username"
                  required
                />
              </div>
              <div class="form-group d-flex align-items-center">
                <label for="password" class="mr-2">비밀번호:</label>
                <input
                  type="password"
                  class="form-control flex-grow"
                  id="password"
                  v-model="password"
                  required
                />
              </div>
              <button type="button" class="btn btn-primary" @click="login">로그인</button>
              <p v-if="loginError" class="text-danger">{{ loginError }}</p>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "LoginView",
  components: {},
  data() {
    return {
        username:'',
        password:'',
        loginError: '',
    };
  },
  methods: {
    login() {
      this.$store.commit("loginUser", {
        username: this.username,
        password: this.password,
      });
      console.log("결과", this.$store.state.user);

      // 로그인 결과 처리
      if(this.$store.state.user === null) {
        this.username='';
        this.password='';
        this.loginError = '아이디나 비밀번호가 올바르지 않습니다.';
      } else {
        // 로그인 성공 시 페이지 이동 등의 처리
        this.$router.push('/');
      }
    },
  },
};
</script>

<style scoped></style>
