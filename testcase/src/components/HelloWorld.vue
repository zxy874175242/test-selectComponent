<template>
  <div class="hello">
    {{chosenList}}
    <select-person :res-list="resList" :chosen-list.sync="chosenList"></select-person>
  </div>
</template>

<script>
import SelectPerson from "./SelectPerson";
export default {
  name: 'HelloWorld',
  components:{
    SelectPerson,
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      resList: [],
      chosenList: [],
    }
  },
  created() {
    this.$axios.get('/api/select', {
      params: {}
    }).then(res => {
      // console.log(res.data.data);
      this.resList = res.data.data.list;
    }).catch(err => {

    });
  },
  mounted() {

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.hello{
  /*display: flex;*/
  /*flex-direction: column;*/
  /*justify-content: center;*/
  /*align-items: center;*/
  font-family: ‘Noto Sans SC’;
  font-weight: normal;
}
</style>
