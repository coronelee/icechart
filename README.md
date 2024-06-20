### only for vue3
### HOW TO USE 

```sh
npm i icechart

import { BarChart } from 'icechart'
 


Use these passed parameters for styling the chart and for passing values.
Be careful! The length of the timeline array should be equal to the length of the values array.

    <BarChart ... />

    width: string `for example -500px-` 
    height: string `for example -500px-` 
    bgColor: string `for example -#123456-` 
    lineColor: string `for example -#123456-` 
    colorText: string `for example -#123456-` 


    !The following values are set as a percentage
    lineWidth: number `for example -1-`   
    borderRadiusLine: number `for example -1-`  
    borderRaduisDiagram: number `for example -1-`  

    :data: object `for example -{timeline: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10], values: [10, 20, 2, 3, 15, 66, 12,1 ,9 ,8]}-`

    see the example below and repeat 

    <BarChart width="500px" height="500px" bgColor="#fcbf49" lineColor="#cdb4db" lineWidth="5" borderRadiusLine="5"
        borderRaduisDiagram="5" colorText="#003049"
        :data="{ timeline: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10], values: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10] }" />
    
```