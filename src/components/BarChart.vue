<template>
    <div>
        <div id="main">
            <div id="quantity"><span v-for="i in toRaw(quantity)" :key="i">{{ i }}</span></div>

            <div id="diagram">
                <div id="gridContainer" v-if="gridState == true"></div>
            </div>
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
const valuesDiagram = ref();
const quantity = ref();
onMounted(() => {
    let diagram = document.getElementById('diagram');
    let main = document.getElementById('main');
    let gridContainer = document.getElementById('gridContainer')

    for (let i = 0; i < props.data.timeline.length; i++) {
        let line = document.createElement('div');
        line.style.width = props.lineWidth / props.data.timeline.length + '%';
        line.style.height = props.data.values[i] / Math.max(...props.data.values) * 100 + '%';
        line.style.backgroundColor = props.lineColor;
        line.style.borderRadius = props.borderRadiusLine + 'px';
        line.style.zIndex = 10

        diagram.appendChild(line);
    }

    quantity.value = props.data.values.sort(function (a, b) { return a - b }).reverse();
    quantity.value = [...new Set(quantity.value)];

    main.style.color = props.colorText;
    main.style.width = props.width;
    main.style.height = props.height;
    main.style.backgroundColor = props.bgColor;
    main.style.borderRadius = props.borderRaduisDiagram + 'px';

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

const repeat = (n, x) => {
    return Array(n).fill(x)
}
</script>

<style scoped>
#main {
    display: grid;
    grid-auto-columns: 1fr;
    grid-template-columns: 0.3fr 2.7fr;
    grid-template-rows: 2.7fr 0.3fr;
    gap: 0px 0px;
    grid-template-areas:
        "quantity diagram"
        "zero timeline";
    padding: 10px;
    font-family: 'Courier New', Courier, monospace;
}

#gridContainer {
    position: absolute;
    display: grid;
    width: 100%;
    height: 100%;
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
    justify-content: space-between;
    align-items: center;
}

#timeline span {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
}

#diagram {
    grid-area: diagram;
    display: flex;
    align-items: end;
    justify-content: space-around;
    position: relative;
}

#zero {
    grid-area: zero;
    display: flex;
    ;
    justify-content: center;
    align-items: center;
}
</style>
