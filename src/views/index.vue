<template>
<el-container>
  <el-aside>
    <el-menu :default-active="1" @select="handleSelect">
      <el-menu-item v-for="(item,index) in navInfo" :key="index" :index="item.index">
      	{{item.name}}
      </el-menu-item>
    </el-menu>
  </el-aside>
  <el-container>
    <router-view></router-view>
  </el-container>
</el-container>
</template>
<script>
export default {
	name: 'index',
	data () {
      return {
      	navInfo: [
      		{
      			index: 1,
      			name: '导航一'
      		},
      		{
      			index: 2,
      			name: '导航二'
      		},
      		{
      			index: 3,
      			name: '导航三'
      		}
      	]
      }
   },
   mounted () {

   },
    methods: {
      handleSelect(key){
      	if(key == 1){
      		this.$router.push('/One');
      	}else if(key == 2){
      		this.$router.push('/Two')
      	}else if(key == 3){
      		this.$router.push('/Three')
      	}
      }
    }  
}
</script>

<style lang="scss" scoped>
.el-container{
	border:solid 1px #ddd;
	height: 500px;
	.el-container{
		border-top:none;
		border-right:none;
		border-bottom: none;
	}
}
.el-header {
   background-color: #B3C0D1;
   color: #333;
   line-height: 60px;
}
.el-aside {
  color: #333;
  width: 200px;
}
.el-menu{
	border-right: none;
}
</style>