<template>
<div>
	<div id="myChart" class="charts"></div>
	<el-row>
	  <el-col :span="10">
	  	<el-input v-model="value" placeholder="请输入名称"></el-input>
	  </el-col>
	  <el-col :span="10">
	  	<el-input v-model="input" type='number' placeholder="请输入数量"></el-input>
	  </el-col>
	  <el-col :span="4">
	  	 <el-button type="primary" @click="changeData">添加数据</el-button>
	  </el-col>
	</el-row>
</div>
  
</template>

<script>
export default {
  name: 'one',
  data () {
    return {
      taskStateList: '',
      value: '',
      state: [],
      number: [],
      input: ''
    }
  },
  mounted () {
  	this.$nextTick(function(){
   		this.getData()
   	})
    
  },
  methods: {
    drawLine(){
		this.state = []
		this.number = []
		this.taskStateList.forEach((item)=>{
			this.state.push(item.state)
			this.number.push(item.number)
		})
		let len = this.taskStateList.length
		localStorage.setItem('state',this.taskStateList[len-1].state)
		localStorage.setItem('number',this.taskStateList[len-1].number)
        // 基于准备好的dom，初始化echarts实例
        let myChart = this.$echarts.init(document.getElementById('myChart'))
        // 绘制图表
        myChart.setOption({
            title: { text: '柱状图' },
            tooltip: {},
            xAxis: {
                data: this.state
            },
            yAxis: {},
            series: [{
                name: '任务完成情况',
                type: 'bar',
                data: this.number
            }]
        });
    },
    getData(){
			this.axios.get('api/stateList',{
				'taskId': 109
			}).then((res) => {
				this.taskStateList = res.data.data.stateList
				console.log(this.taskStateList)
				localStorage.setItem('taskStateList',this.taskStateList)
				this.drawLine()
			})
		},
	changeData(){
		if(this.value==''){
			alert('名称不能为空');
			return false;
		}
		if(this.input == ''){
			alert('数量不能为空');
			return false;
		}
		this.taskStateList.push({
			state: this.value,
			number: this.input
		})
		 localStorage.setItem('taskStateList',this.taskStateList)
		 console.log(this.taskStateList)
		 this.drawLine()
		 this.$message({
      message: '恭喜你，添加成功消息',
      type: 'success'
    });
    this.value = ''
    this.input = ''	
	}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
.charts{
	width: 800px;
	height: 400px;
}
</style>
