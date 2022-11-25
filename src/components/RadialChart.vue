<template>
	<div :id="id" class="className" :style="{height:height,width:width}" />
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
	}
	},
	data() {
		return {
			chart: null,
			value: 30, 
			valueColor: 'red',
			insideColor: ['blue', 'grey'],
			outsideValue1: 80, outsideValue2: 10,
			outsideColor: [ 'green', 'orange', 'red'],
		}
	},
	mounted() {
		this.initChart()
	},
	beforeDestroy() {
		if (!this.chart) {
			return
		}
		this.chart.dispose()
		this.chart = null
	},
	methods: {
		initChart() {
			this.chart = echarts.init(document.getElementById(this.id))
			this.chart.setOption({
				title: {
					text: this.value + "%",
					subtext: "Core 2",
					subtextStyle : {
						color: 'red'
						// fontStyle: 'normal',
						// fontWeight: 'normal',
						// fontSize: 12,
						// verticalAlign: top
					},
					left: "center",
					top: "center",
					textStyle: {
						fontSize: 30,
						color: this.valueColor

					},
					subtextStyle: {
						fontSize: 20
					}
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