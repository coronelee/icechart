<template>
    <ul class='pie'>
        <li class='slice'>
            <div class='slice-contents'></div>
        </li>
        <!-- you can add more slices here -->
    </ul>
</template>

<script setup>
import { onMounted } from "vue";


const props = defineProps({
    width: String,
    height: String,
    data: Array,
    bgColor: Array
});

onMounted(() => {

    const max = Math.max(...props.data);
    const pie = document.getElementById('pie');
    console.log(props.data.length)

    for (let i = 0; i < props.data.length; i++) {
        let slice = document.createElement('li');
        let sliceContents = document.createElement('div');
        slice.classList.add('slice');
        sliceContents.classList.add('slice-contents');
        sliceContents.style.backgroundColor = props.bgColor[i];
        sliceContents.style.height = (props.data[i] / max) * 100 + '%';
        slice.appendChild(sliceContents);
        pie.appendChild(slice);
    }

})

</script>



<!-- <script setup>
import { onMounted, ref, toRaw } from "vue"
import { errorMessages } from "vue/compiler-sfc";

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
});
const valuesDiagram = ref();
const quantity = ref();
onMounted(() => {
    if (props.data.timeline.length != props.data.values.length) {
        return alert("timeline and values must be the same length");
    } else {
        let diagram = document.getElementById('diagram');
        let main = document.getElementById('main');

        for (let i = 0; i < props.data.timeline.length; i++) {
            let line = document.createElement('div');
            line.style.width = props.lineWidth + 'px';
            line.style.height = props.data.values[i] / Math.max(...props.data.values) * 100 + '%';
            line.style.backgroundColor = props.lineColor;
            line.style.borderRadius = props.borderRadiusLine + 'px';
            diagram.appendChild(line);
        }


        props.data.timeline = [...new Set(props.data.timeline)];
        quantity.value = props.data.values.sort(function (a, b) { return a - b }).reverse();
        quantity.value = [...new Set(quantity.value)];



        main.style.color = props.colorText;
        main.style.width = props.width;
        main.style.height = props.height;
        main.style.backgroundColor = props.bgColor;
        main.style.borderRadius = props.borderRaduisDiagram + 'px';

        diagram.style.gridTemplateColumns = `repeat(${props.data.timeline.length}, 1fr)`;
        diagram.style.gridTemplateRows = `repeat(${quantity.value.length}, 1fr)`;
    }






}) 

const repeat = (n, x) => {
return Array(n).fill(x)
}
</script>
-->
<style scoped>
.pie {
    overflow: hidden;
    position: relative;
    margin: 1em auto;
    border: dashed 1px;
    padding: 0;
    width: 32em;
    height: 32em;
    border-radius: 50%;
    list-style: none;
}

.slice {
    overflow: hidden;
    position: absolute;
    top: 0;
    right: 0;
    width: 50%;
    height: 50%;
    transform-origin: 0% 100%;
}

.slice:first-child {
    transform: rotate(15deg) skewY(-22.5deg);
}

.slice:nth-child(2) {
    transform: rotate(60deg) skewY(-22.5deg);
    background-color: aqua;
}

.slice:nth-child(3) {
    transform: rotate(105deg) skewY(-22.5deg);
    background-color: blue;
}

.slice-contents {
    position: absolute;
    left: -100%;
    width: 200%;
    height: 200%;
    border-radius: 50%;
    background: lightblue;
}

.slice:first-child .slice-contents {
    transform: skewY(22.5deg);
    /* unskew slice contents */
}

.slice:hover .slice-contents {
    background: violet;
}

/* highlight on hover */
</style>
