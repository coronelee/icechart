<template>
    <div id="container">


        <LineChart width="500px" height="300px" bgColor="#fcbf49" lineColor="red" lineWidth="1" borderRadiusLine="5"
            borderRaduisDiagram="5" colorText="#003049"
            :data="{ timeline: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11], values: [0, 2, 3, 4, 5, 2, 1, 2, 8, 2, 1] }"
            :gridState=true />
    </div>


</template>

<script setup>
import BarChart from './components/BarChart.vue';
import CircleChart from './components/CircleChart.vue';
import LineChart from './components/LineChart.vue';
</script>

<style scoped>
.container {
    position: absolute;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100vw;
    height: 100vh;
}
</style>