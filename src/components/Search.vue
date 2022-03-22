<template>
  <div class="box">
    <h3 class="searchTitle">Search Github Users</h3>
    <div class="boxsearch">
      <input
        class="searchInput"
        type="text"
        placeholder="enier the name you search"
        v-model="keyword"
      />
      <button @click="mySearch">search</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios' 
export default {
  name: "Search",
  data() {
      return{
          keyword:''
      }
  },
  methods:{
      mySearch(){
          this.$bus.$emit('listUsers',{isHello:false,isDown:true,error:'',users:[]})
          axios.get('http://api.github.com/search/users?q=' + this.keyword).then(
              response => {
                  console.log('请求成功了')
                  this.$bus.$emit('listUsers',{isDown:false,error:'',users:response.data.items})
              },
              error => {
                  console.log('qingqiu',error.massage)
                  this.$bus.$emit('listUsers',{isDown:false,error:error.massage,users:[]})
              }
          )
      }
  }
};
</script>

<style scoped>
.box {
  width: 600px;
  height: 100px;
  background: rgba(0, 0, 0, 0.2);
  margin: 20px auto;
}
.searchTitle {
  padding-top: 10px;
  padding-left: 20px;
}
.boxsearch {
  padding-left: 20px;
}
.searchInput {
  border: none;
  border-bottom: 1px solid #000;
  outline: none;
  color: rgba(0, 0, 0, 0.2);
  margin: 2px;
}
</style>