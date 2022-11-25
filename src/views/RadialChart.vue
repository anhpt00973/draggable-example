<template>
	<!-- <div > -->
	<div class="chart-container">
	  <chart divId="0" valueX="10"
	  height="250px" width="250px" />
	  <chart divId="1" valueX="50"
	  height="250px" width="250px" />
	  <chart divId="2" valueX="20"
	  height="250px" width="250px" />
	  <chart divId="3" valueX="60"
	  height="250px" width="250px" />
	  <chart divId="4" valueX="70"
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
	display: inline-flex;
	position: relative;
	width: 100%;
	height: calc(100vh - 84px);
 }
 </style>
 