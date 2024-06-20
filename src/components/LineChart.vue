<template>
    <div>
        <div id="main">
            <div id="quantity"><span v-for="i in toRaw(quantity)" :key="i">{{ i }}</span></div>


            <canvas id="canvas">
                <div id="gridContainer" v-if="gridState == true"></div>

            </canvas>

            <div id="zero">
                0
            </div>
            <div id="timeline"><span v-for="i in data.timeline" :key="i">{{ i }}</span></div>
        </div>
        <!-- <div v-else :style="['background-color:' + props.bgColor, 'padding: 10px']">
            <p>timeline and values must be the same length</p>
        </div> -->
    </div>

</template>

<script setup>
import { onMounted, ref, toRaw } from "vue"

const props = defineProps({
    width: String,
    height: String,
    bgColor: String,
    lineColor: String,
    lineWidth: Number,
    data: Object,
    borderRadiusLine: Number,
    borderRaduisDiagram: Number,
    colorText: String,
    gridState: Boolean
});

const quantity = ref();

onMounted(() => {
    let main = document.getElementById('main');
    let gridContainer = document.getElementById('gridContainer')

    main.style.width = props.width;
    main.style.height = props.height;
    let canvas = document.getElementById("canvas");
    canvas.style.backgroundColor = 'transparent';
    canvas.width = props.width.split('px')[0] - 50;
    canvas.height = props.height.split('px')[0];
    let ctx = canvas.getContext("2d");

    ctx.beginPath();
    ctx.moveTo(0, canvas.height - (props.data.values[0] / Math.max(...props.data.values) * canvas.height));

    for (let i = 1; i < props.data.timeline.length; i++) {
        const x = (i / (props.data.timeline.length - 1)) * canvas.width;
        const y = canvas.height - (props.data.values[i] / Math.max(...props.data.values) * canvas.height);
        ctx.lineTo(x, y);
    }

    ctx.stroke();
    ctx.closePath();

    quantity.value = props.data.values.sort(function (a, b) { return a - b }).reverse();
    quantity.value = [...new Set(quantity.value)];

    gridContainer.style.gridTemplateColumns = `repeat(${props.data.timeline.length}, 1fr)`;
    gridContainer.style.gridTemplateRows = `repeat(${quantity.value.length}, 1fr)`;

    for (let i = 0; i < (quantity.value.length * props.data.timeline.length); i++) {
        let gridDiv = document.createElement('div')
        gridDiv.style.width = '100%'
        gridDiv.style.height = '100%'
        gridDiv.style.border = '.6px gray solid'
        gridContainer.appendChild(gridDiv)
    }

})



</script>

<style scoped>
#main {
    display: grid;
    grid-auto-columns: 1fr;
    grid-template-columns: 0.3fr 2.7fr;
    grid-template-rows: 2.7fr 0.3fr;
    gap: 0px 0px;
    grid-template-areas:
        "quantity canvas"
        "zero timeline";
    padding: 10px;
    font-family: 'Courier New', Courier, monospace;
}

#gridContainer {
    position: absolute;
    display: grid;
    width: 100%;
    height: 100%;
    z-index: 10;
}

#quantity {
    grid-area: quantity;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    align-items: center;
}

#quantity span {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: start;
}

#timeline {
    grid-area: timeline;
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    align-items: center;
}

#timeline span {
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
}

#canvas {
    grid-area: canvas;
    display: flex;
    align-items: end;
    width: 100%;
    height: 100%;
    position: relative;
    /* transform: rotate(-180deg); */
}

#zero {
    grid-area: zero;
    display: flex;
    ;
    justify-content: center;
    align-items: center;
}
</style>
