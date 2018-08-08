<template>
    <div>
      <h1>课程列表</h1>
      <ul v-for="item in courseList">
        <li>{{item.name}}</li>
      </ul>
    </div>
</template>

<script>
    export default {
        name: "Course",
        data(){
          return {
            courseList:[
              {id:1,title:'傻逼'},
              {id:2,title:'猪肉'},
            ]
          }
        },
      mounted(){
          this.initCourse();
          this.testCors();
      },
      methods:{
          initCourse:function () {
            var that = this
            this.$axios.request({
              url:'http://127.0.0.1:8000/api/v1/courses/',
              method:'GET',
              responseType:'json'
            }).then(function (arg) {
              if (arg.data.code === 1000){
                that.courseList = arg.data.data
              } else{
                alert(arg.data.error);
              }
            }).catch(function (arg) {

            })
          },
          testCors:function () {
            this.$axios.request({
              url: 'http://127.0.0.1:8000/api/v1/auth/',
              method: 'POST',
              headers:{
                'Content-Type':'application/json',
                'xxxxx':123,
              },
              responseType: 'json'
            }).then(function (arg) {
              console.log(123);
            }).catch(function (arg) {

            })
          }
      }
    }
</script>

<style scoped>

</style>
