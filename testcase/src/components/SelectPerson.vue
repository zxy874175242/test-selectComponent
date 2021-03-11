<template>
  <div class="layer">
<!--    {{resList}}-->
<!--    {{this.value}}-->

    <div class="display-mode">
      <div style="margin: 0px 15px 0px 5px;height: 24px;line-height: 24px">待选人员</div>
      <div v-for="item in chosenListFull" class="person-cell-hover" @click="chooseByList(item.id)">
        {{ item.name }}
        <div class="delete-icon"><i class="el-icon-close"></i></div>
      </div>
<!--      <button class="button-circle" @click="isSelect = ! isSelect"><i class="el-icon-edit"></i></button>-->
      <el-button style="margin-left: 15px" size="small" type="primary" circle @click="toSelect"><i class="el-icon-edit"></i></el-button>
    </div>
    <transition name="slide-fade">
      <div class="select-mode" v-if="isSelect">
      <el-input
        placeholder="搜索"
        prefix-icon="el-icon-search"
        v-model="input">
      </el-input>
      <div class="name-list">
        <div v-for="(item,index) in searchResList">
          <div class="person-cell" @click="chooseByList(item.id)" v-if="value.indexOf(item.id) === -1">{{ item.name }}</div>
          <div class="person-cell-chosen" @click="chooseByList(item.id)" v-else>{{ item.name }}</div>
        </div>
      </div>
      <div style="flex: 1"></div>
      <el-button type="primary" style="width: 100%;margin-bottom: 0" @click="applyRes">确定</el-button>

    </div>
    </transition>

  </div>

</template>

<script>
export default {
  name: "Select",
  data() {
    return {
      value:[],
      input: "",
      isSelect: true,
      test: 0,
      chosenListFull: [],
      searchResList: [],
    }
  },
  props: ['resList','chosenList'],
  watch: {
    input(val,oldVal) {
      let keyY = new RegExp(val,'gm')
      this.searchResList = this.resList.filter(e =>  keyY.test(e.name) );
      // console.log('change',this.searchResList);
    },
    resList(val,oldVal){
      this.initData();
    },
    value(val,oldVal){
      this.chosenListFull = this.resList.filter(e => this.value.indexOf(e.id) !== -1);
    }
  },
  mounted() {


    let _this = this;
    this.value = [...this.chosenList];
    // this.value = this.chosenList;


    if(this.resList !== null){
      _this.chosenListFull = _this.resList.filter(e => _this.value.indexOf(e.id) !== -1);
    }

  },
  methods: {
    initData() {
      this.chosenListFull = this.resList.filter(e => this.value.indexOf(e.id) !== -1);
      this.searchResList = this.resList;
    },
    chooseByList(id) {
      let num = this.value.indexOf(id);
      if(num === -1){
        this.value.push(id);
      }else {
        this.value.splice(num,1);
      }
      this.$emit('update:chosenList',[...this.value]);

    },
    applyRes(){
      this.isSelect = false;
      // this.$emit('update:chosenList',[...this.value]);
    },
    toSelect(){
      this.isSelect = !this.isSelect;
      // this.$emit('update:chosenList',[...this.value]);
    }
  }
}
</script>

<style scoped>

  .layer {
    letter-spacing: 0.5px;
    width: 800px;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
  }
  .display-mode {
    /*min-height: 50px;*/
    /*width: 500px;*/
    text-align: center;
    line-height: 50px;
    display: flex;
    flex-direction: row;
    align-items: center;
    flex-wrap: wrap;
    margin-bottom: 15px;
    margin-top: 10px;
  }
  .select-mode {
    display: flex;
    flex-direction: column;
    width: 500px;
    min-height: 300px;
    background-color: white;
    box-shadow: 0px 0px 50px rgba(0,0,0,0.05);
    border-radius: 10px;
    box-sizing: border-box;
    padding: 15px 15px;
  }
  .person-cell {
    box-sizing: border-box;
    height: 24px;
    /*width: 100px;*/
    border-radius: 5px;
    background-color: rgb(241,249,255);
    padding: 0px 10px;
    margin: 5px 5px;
    border: rgb(47,151,241) 1px solid;
    color: rgb(47,151,241);
    line-height: 22px;
    align-items: center;
    font-size: 14px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  .person-cell-chosen {
    box-sizing: border-box;
    height: 24px;
    /*width: 100px;*/
    border-radius: 5px;
    background-color: rgb(47,151,241);
    padding: 0px 10px;
    margin: 5px 5px;
    border: rgb(47,151,241) 1px solid;
    color: rgb(241,249,255);
    line-height: 22px;
    align-items: center;
    font-size: 14px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  .person-cell-hover {
    box-sizing: border-box;
    height: 24px;
    /*width: 100px;*/
    border-radius: 5px;
    background-color: rgb(241,249,255);
    padding: 0px 10px;
    margin: 5px 5px;
    border: rgb(47,151,241) 1px solid;
    color: rgb(47,151,241);
    line-height: 22px;
    align-items: center;
    font-size: 14px;
    cursor: pointer;
    transition: all 0.2s ease;
    text-align: center;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .person-cell-hover:hover{
    border: #F15B67 1px solid;
    color: rgba(47,151,241,0.3);
    background-color: white;
  }



  .button-circle {
    width: 28px;
    height: 28px;
    border-radius: 50%;
    font-size: 16px;
  }
  .name-list {
    margin: 10px 0px;
    display: flex;
    flex-wrap: wrap;
    flex: 0;
  }
  .delete-icon{
    position: absolute;
    color: transparent;
    transition: all 0.2s ease;
  }

  .person-cell-hover:hover .delete-icon{
    color: #F15B67;
  }

  .slide-fade-enter-active {
    transition: all .2s ease;
  }
  .slide-fade-leave-active {
    transition: all .2s cubic-bezier(1.0, 0.5, 0.8, 1.0);
  }
  .slide-fade-enter, .slide-fade-leave-to
    /* .slide-fade-leave-active for below version 2.1.8 */ {
    transform: translateY(-10px);
    opacity: 0;
  }
</style>
