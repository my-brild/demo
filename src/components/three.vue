<template>
<div>
	<div id="myChart" class="charts"></div>
</div>
  
</template>

<script>
export default {
  name: 'one',
  data () {
    return {
      taskStateList: '',
      state: [],
      number: []
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
		this.taskStateList.forEach((item,index)=>{
			if(index<10){
				this.state.push(item.state)
				this.number.push(item.number)
				
			}
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
