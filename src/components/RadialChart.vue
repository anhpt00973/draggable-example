<template>
<!-- <div> -->
	<div :id="divId" :valueX="valueX" class="className" :style="{height:height,width:width}" />
<!-- </div> -->
</template>

<script>
import echarts from 'echarts'
import resize from './mixins/resize'

export default {
	// mixins: [resize],
	props: {
		className: {
			type: String,
			default: 'chart'
		},
		id: {
			type: String,
			default: 'chart'
		},
		width: {
			type: String,
			default: '200px'
		},
		height: {
			type: String,
			default: '200px'
		},
		divId: {
			type: String,
			default: '0' 
		},
		valueX: {
			type: String,
			default: '0'
		}
	},
	data() {
		return {
			myChart: null,
			value: 30, 
			valueColor: 'red',
			insideColor: ['blue', 'grey'],
			outsideValue1: 80, outsideValue2: 10,
			outsideColor: [ 'green', 'orange', 'red']
			
		}
	},
	mounted() {
		let vm = this
		vm.initChart(vm.divId, vm.valueX)
	},
	beforeDestroy() {
		let vm = this
		if (!vm.myChart) {
			return
		}
		vm.myChart.dispose()
		vm.myChart = null
	},
	methods: {
		initChart(divId, valueX) {
			let vm = this
			vm.myChart = echarts.init(document.getElementById(vm.divId))
			vm.myChart.setOption({
				title: {
					text: this.valueX + "%",
					subtext: "Core 2",
					subtextStyle : {
						color: 'red',
						fontStyle: 'normal',
						fontWeight: 'bold',
						fontSize: 15,
						// verticalAlign: 
					},
					left: "center",
					top: "center",
					textStyle: {
						fontSize: 30,
						color: this.valueColor

					},
				},
				chart: {
					height: 180,
					type: 'radialBar',
					offsetY: 20,
					sparkline: {
						enabled: true
					}
				},
				tooltip: {
					trigger: 'item',
					formatter: '{a} <br/>{b}: {c} ({d}%)'
				},
				series: [
					{
						startAngle: -17,
						name: 'Access From',
						type: 'pie',
						selectedMode: 'single',
						radius: ['30%', '41%'],
						label: {
							position: 'inner',
							fontSize: 14
						},
						data: [
						{
							value: 40,
							selected: false,
							itemStyle: {
								opacity: 0
							}
						},
						{ value: this.value*60/100, itemStyle: { color: this.insideColor[0] } }, 
						{ value: 60 - this.value*60/100, itemStyle: { color: this.insideColor[1] } }
						]
					},
					{
						startAngle: -17,
						name: 'Access From',
						type: 'pie',
						radius: ['42%', '44%'],
						labelLine: {
						show: false
						},
						data: [
						{
							value: 40,
							itemStyle: {
								color: 'black',
								opacity: 0
							}
						},
						{ value: this.outsideValue1*60/100, itemStyle: { color: this.outsideColor[0] } },
						{ value: this.outsideValue2*60/100, itemStyle: { color: this.outsideColor[1] } },
						{ value: (60-this.outsideValue1*60/100-this.outsideValue2*60/100), itemStyle: { color: this.outsideColor[2] } }
						]
					}
				]
			})
		}
	}
}
</script>