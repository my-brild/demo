<template>
  <div>
   <div id="myChart" class="charts"></div>
  </div>
</template>

<script>
export default {
  name: 'two',
  data () {
    return {
      state: [],
      number: []
    }
  },
  mounted () {
  	this.$nextTick(function(){
   		this.drawLine()
   	})
    
  },
  methods: {
    drawLine(){
    	this.state.push(localStorage.getItem('state'))
    	this.number.push(localStorage.getItem('number'))
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
