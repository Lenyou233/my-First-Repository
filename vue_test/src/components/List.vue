<template>
  <div class="box">
    <div v-show="info.isHello">欢迎使用</div>
    <div v-show="info.isDown">加载中，请稍后...</div>
    <div v-show="info.error">
      {{ info.error }}
    </div>
    <ul>
      <li class="boxli" v-for="user in info.users" :key="user.id">
        <a :href="user.html_url" target="_blank">
          <img :src="user.avatar_url" alt="" style="width: 150px" />
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "List",
  data() {
    return {
      info: {
        users: [],
        isHello: true,
        isDown: false,
        error: "",
      },
    };
  },
  mounted() {
    this.$bus.$on("listUsers", (dataObj) => (this.info = dataObj));
  },
};
</script>

<style scoped>
.box {
  width: 580px;
  margin: 20px auto;
  padding: 10px;
}
.boxli {
  float: left;
  width: 160px;
  height: 160px;
  list-style: none;
  margin: 2px;
}
</style>