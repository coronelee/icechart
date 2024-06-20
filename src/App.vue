<template>
    <!-- <BarChart width="50%" height="500px" bgColor="#fcbf49" lineColor="#cdb4db" lineWidth="20" borderRadiusLine="5"
        borderRaduisDiagram="5" colorText="#003049"
        :data="{ timeline: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10], values: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10] }"
        :gridState=true /> -->
    <LineChart width="500px" height="300px" bgColor="#fcbf49" lineColor="#ccc" lineWidth="1" borderRadiusLine="5"
        borderRaduisDiagram="5" colorText="#003049"
        :data="{ timeline: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11], values: [1, 2, 1, 2, 1, 2, 1, 2, 1, 2, 1] }"
        :gridState=true />



</template>

<script setup>
import BarChart from './components/BarChart.vue';
import CircleChart from './components/CircleChart.vue';
import LineChart from './components/LineChart.vue';
</script>

<style scoped>
.container {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100vw;
    height: 100vh;
}
</style>