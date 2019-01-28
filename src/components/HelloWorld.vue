<template>
	<div class='index'>
		<div class="container">
			我是头部
		</div>
		<div id="main"></div>
		<div class="date">
			<input type="text" @focus="openPicker" class="dateInp" placeholder="请选择时间" v-model="pickerValue">
			<template>
				<mt-datetime-picker
					ref="picker"
					type="date"
					@confirm="handleConfirm"
					>
				</mt-datetime-picker>
			</template>
		</div>
		<div class="footer">
			我是底部
		</div>
	</div>
</template>
<script>
// 按需引入echarts
// 引入 ECharts 主模块
var echarts = require('echarts/lib/echarts');
// 引入柱状图
require('echarts/lib/chart/bar');
// 引入提示框和标题组件
require('echarts/lib/component/tooltip');
require('echarts/lib/component/title');

	export default {
		name: 'index',
		props: {

		},
		data () {
			return {
				 pickerValue:""
			}
		},
		methods: {
			openPicker() {
        this.$refs.picker.open();
			},
			handleConfirm(val) {
				var month = val.getMonth()+1<10?`0${val.getMonth()+1}`:val.getMonth()+1
				var day = val.getDate()<10?`0${val.getDate()}`:val.getDate()
				this.pickerValue = `${val.getFullYear()}-${month}-${day}`
			}
		},
		created() {

		},
		mounted() {
			// var scale = 1 / devicePixelRatio;
			// document.querySelector('meta[name="viewport"]').setAttribute('content','initial-scale=' + scale + ', maximum-scale=' + scale + ', minimum-scale=' + scale + ', user-scalable=no');
			// 基于准备好的dom，初始化echarts实例
			var myChart = echarts.init(document.getElementById('main'));
			// 绘制图表
			myChart.setOption({
					title: {
							text: 'ECharts 入门示例'
					},
					tooltip: {},
					xAxis: {
							data: ['衬衫', '羊毛衫', '雪纺衫', '裤子', '高跟鞋', '袜子']
					},
					yAxis: {},
					series: [{
							name: '销量',
							type: 'bar',
							data: [5, 20, 36, 10, 10, 20]
					}]
			});

		},
		watch: {

		},
		components: {
		}
	}
</script>
<style scoped lang="less">
.index{
	width: 100%;
	height: 100%;
	// background-color: red;
	.container {
		width: 375px;
		height: 100px;
		line-height: 100px;
		text-align: center;
		background-color: rgb(0, 204, 255);
		font-size: 24px;
		margin-bottom: 75px;
	}
	#main {
		width: 750px;
		height: 600px;
	}
	.date {
		width: 700px;
		margin: 20px auto;
	}
	.footer {
		margin: 0 auto;
		width: 700px;
		height: 50px;
		line-height: 50px;
		font-size: 24px;
		text-align: center;
		background-color: yellowgreen;
	}
}
</style>