<template>
	 <!-- <li class="list-group-item" v-for="element in list" :key="element.order">
            <i :class="element.fixed? 'fa fa-anchor' : 'glyphicon glyphicon-pushpin'" @click=" element.fixed=! element.fixed" aria-hidden="true"></i>
            {{element.name}}
            <span class="badge">{{element.order}}</span>
          </li> -->
	<div class="chart-container" 
		style="display: inline-flex;
		position: relative;
		width: 100%;
		height: calc(100vh - 84px);">
	   <li class="list-group-item" v-for="item in listData" :key="item.index">
			<i>
				<chart  :divId="item.index" :valueX="item.value" :nameX="item.name"
				height="250px" width="250px" 
					style="margin-right:-50px;margin-left:-50px;margin-top:-50px;margin-bottom:-300px;"
				/>
			</i>
		</li>
	</div>
 </template>
 
 <script>
 import Chart from '@/components/RadialChart'
 
 export default {
	name: 'KeyboardChart',
	components: { Chart },
	data() {
		return {
			listData: [
				{ index: '0', value: '10', name: 'core1', fixed: false },
				{ index: '1', value: '20', name: 'core2', fixed: false },
				{ index: '2', value: '30', name: 'core3', fixed: false },
				{ index: '3', value: '40', name: 'core4', fixed: false },
				{ index: '4', value: '50', name: 'core5', fixed: false },
				{ index: '5', value: '60', name: 'core6', fixed: false }
			]
		}
	}
 }
 </script>
 
 <style scoped>
 .chart-container{
	
 }
 </style>
 