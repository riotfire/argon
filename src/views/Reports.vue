<template>
    <div>
        <base-header type="gradient-success" class="pb-6 pb-8 pt-5 pt-md-8">
            <!-- Card stats -->
            <div class="row">
                <div class="col-xl-3 col-lg-6">
                    <stats-card title="Hand Washing Audits"
                                type="gradient-blue"
                                sub-title="22"
                                icon="ni ni-active-40"
                                class="mb-4 mb-xl-0"
                    >

                        <template slot="footer">
                            <span class="text-danger mr-1">28</span>
                            <span class="text-nowrap">to go this month</span>
                        </template>
                    </stats-card>
                </div>
                <div class="col-xl-3 col-lg-6">
                    <stats-card title="Hand Wash Compliance"
                                type="gradient-orange"
                                sub-title="32%"
                                icon="ni ni-like-2"
                                class="mb-4 mb-xl-0"
                    >

                        <template slot="footer">
                            <span class="text-success mr-1"><i class="fa fa-arrow-up"></i> 12.18%</span>
                            <span class="text-nowrap">Since last month</span>
                        </template>
                    </stats-card>
                </div>
                <div class="col-xl-3 col-lg-6">
                    <stats-card title="PPE Audits"
                                type="gradient-green"
                                sub-title="3"
                                icon="ni ni-umbrella-13"
                                class="mb-4 mb-xl-0"
                    >

                        <template slot="footer">
                            <span class="text-danger mr-1">17</span>
                            <span class="text-nowrap">to go this month</span>
                        </template>
                    </stats-card>

                </div>
                <div class="col-xl-3 col-lg-6">
                <stats-card title="PPE Compliance"
                            type="gradient-purple"
                            sub-title="75%"
                            icon="ni ni-satisfied"
                            class="mb-4 mb-xl-0"
                >

                    <template slot="footer">
                        <span class="text-danger mr-2"><i class="fa fa-arrow-down"></i> 5.72%</span>
                        <span class="text-nowrap">Since last month</span>
                    </template>
                </stats-card>
                </div>
            </div>


        </base-header>

        <!--Charts-->
        <div class="container-fluid mt--7">
            <div class="row">
                <div class="col-xl-4 mb-5 mb-xl-0">
                    <card type="default" header-classes="bg-transparent">
                        <div slot="header" class="row align-items-center">
                            <div class="col">
                                <h6 class="text-light text-uppercase ls-1 mb-1">Handwash Audits</h6>
                                <h5 class="h3 text-white mb-0">Role Distribution</h5>
                            </div>
                        </div>
                        <pie-chart
                                :height="350"
                                ref="bigChart"
                                :chart-data="hwDistroChart.chartData"
                                :extra-options="hwDistroChart.extraOptions"
                        >
                        </pie-chart>

                    </card>
                </div>

                <div class="col-xl-4">
                    <card header-classes="bg-transparent">
                        <div slot="header" class="row align-items-center">
                            <div class="col">
                                <h6 class="text-uppercase text-muted ls-1 mb-1">Performance</h6>
                                <h5 class="h3 mb-0">Hand Hygiene Compliance</h5>
                            </div>
                        </div>

                        <bar-chart
                                :height="350"
                                ref="barChart"
                                :chart-data="hwComplianceChart.chartData"
                        >
                        </bar-chart>
                    </card>
                </div>

                <div class="col-xl-4">
                    <card type="default" header-classes="bg-transparent">
                        <div slot="header" class="row align-items-center">
                            <div class="col">
                                <h6 class="text-uppercase text-light ls-1 mb-1">Improvement</h6>
                                <h5 class="text-white h3 mb-0">Hand Hygiene Compliance</h5>
                            </div>
                        </div>

                        <line-chart
                                :height="350"
                                ref="barChart"
                                :chart-data="redBarChart.chartData"
                                :extra-options="redBarChart.extraOptions"
                        >
                        </line-chart>
                    </card>
                </div>
            </div>
            <!-- End charts-->
        </div>

    </div>
</template>
<script>
  // Charts
  import * as chartConfigs from '@/components/Charts/config';
  import LineChart from '@/components/Charts/LineChart';
  import BarChart from '@/components/Charts/BarChart';
  import PieChart from '@/components/Charts/PieChart';

  export default {
    components: {
      LineChart,
      BarChart,
      PieChart
    },
    data() {
      return {
        bigLineChart: {
          allData: [
            [0, 20, 10, 30, 15, 40, 20, 60, 60],
            [0, 20, 5, 25, 10, 30, 15, 40, 40]
          ],
          activeIndex: 0,
          chartData: {
            datasets: [],
            labels: [],
          },
          extraOptions: chartConfigs.blueChartOptions,
        },
        hwDistroChart: {
          chartData: {
            labels: ['Physician','Nurse','Technician','Student','Dietitian','Social Worker','Other'],
            datasets: [{
              label: 'Sales',
              data: [5, 20, 30, 12, 17, 49, 10],
              backgroundColor: ['#00335F','#005CAC','#1392FE','#5FB5FF','#92CDFF','#C5E4FF','#DFF0FE','#5FB5FF']
            }]
          }
        },
        hwComplianceChart: {
          chartData: {
            labels: ['Physician','Nurse','Technician','Student','Dietitian','Social Worker','Other'],
            datasets: [{
              label: 'Compliance',
              data: [5, 60, 30, 12, 17, 49, 10],
            }]
          }
        },
        redBarChart: {
          chartData: {
            labels: ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug'],
            datasets: [{
              label: '# of Audits',
              data: [0, 20, 5, 25, 10, 30, 15, 40, 40]
            }],
            extraOptions: chartConfigs.blueChartOptions,
          }
        }
      };
    },
    methods: {
      initBigChart(index) {
        let chartData = {
          datasets: [
            {
              label: 'Performance',
              data: this.bigLineChart.allData[index]
            }
          ],
          labels: ['May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
        };
        this.bigLineChart.chartData = chartData;
        this.bigLineChart.activeIndex = index;
      }
    },
    mounted() {
      this.initBigChart(0);
    }
  };
</script>
<style></style>
