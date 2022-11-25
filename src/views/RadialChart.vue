<template>
	<!-- <div > -->
	<div class="chart-container">
	  <chart 
	  height="250px" width="250px" />
	</div>
 <!-- </div> -->
 </template>
 
 <script>
 import Chart from '@/components/RadialChart'
 
 export default {
	name: 'KeyboardChart',
	components: { Chart }
 }
 </script>
 
 <style scoped>
 .chart-container{
	position: relative;
	width: 100%;
	height: calc(100vh - 84px);
 }
 </style>
 