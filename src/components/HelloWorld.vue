<template>
  <div>
    <div class="chart-wrapper d-block m-auto">
    <p class="text-center">Weather</p>
      <chart :options="chartOptionsBar">
    
      </chart>
    </div>
    <hr />

    <!-- <div class="chart-wrapper">
      <chart :options="chartOptionsBar">

      </chart>
    </div> -->

  </div>
</template>

<script>
export default {
  methods: {
  },
  name: "HelloWorld",
  data: () => ({
    chartOptionsBar: {
      xAxis: {
         data: [
          "Sun",
          "Mon",
          "Tue",
          "Wed",
          "Thu",
          "Fri",
          "Sat"  
        ]
      },
      yAxis: {
        type: "value",
        title: "temp",
      },
      series: [
        {
          type: "bar",
          data: [40, 100, 10, 70, 50,  20, 60]
        }
        
      ],

      title: {
        text: "Quarterly Sales Results",
        x: "center",
        textStyle: {
          fontSize: 24
        }
      },
      color: ["#127ac2"]
    }

    // chartOptionsLine: {
    //   xAxis: {
    //     data: [
    //       "Jan",
    //       "Feb",
    //       "Mar",
    //       "Apr",
    //       "May",
    //       "Jun",
    //       "Jul",
    //       "Aug",
    //       "Sep",
    //       "Oct",
    //       "Nov",
    //       "Dec"
    //     ]
    //   },
    //   yAxis: {
    //     type: "value"
    //   },
    //   series: [
    //     {
    //       type: "line",
    //       data: [55, 72, 84, 48, 59, 62, 87, 75, 94, 101, 127, 118]
    //     }
    //   ],
    //   title: {
    //     text: "Monthly Stock Prices",
    //     x: "center",
    //     textStyle: {
    //       fontSize: 24
    //     }
    //   },
    //   color: ["#127ac2"]
    // }
  })
};
</script>

<style scoped>
.chart-wrapper {
  background-color: aliceblue;
  opacity: 60%;
  width: 50%;
  /* height: 60%; */
}



 /* .echarts {
  width: 30%;
  height: 30%;
}  */
</style>
