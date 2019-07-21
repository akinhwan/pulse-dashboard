<template>
  <div>

    <!-- SHORT ROW -->
    <div class="row">
      <div class="col-3">
        <card type="chart" class="shorter-cards">	    
          <template slot="header">	
            <h5 class="card-category">Readmission Rate</h5>	
            <h3 class="card-title">3%</h3>	
            <h5 class="card-title"><i class="tim-icons icon-triangle-right-17 trend-up"></i> .08%</h5>	
          </template>	
          <div class="chart-area">	
            <line-chart style="height: 100%"	
                        chart-id="purple-line-chart"	
                        :chart-data="smallBlueLine.chartData"	
                        :gradient-colors="smallBlueLine.gradientColors"	
                        :gradient-stops="smallBlueLine.gradientStops"	
                        :extra-options="smallBlueLine.extraOptions">	
            </line-chart>	
          </div>	
        </card>
      </div>

      <div class="col-3">
        <card type="chart" class="shorter-cards">	 
          <template slot="header">	
            <h5 class="card-category">Total Patients Admitted</h5>	
            <h3 class="card-title">4,183</h3>	
            <h5 class="card-title"><i class="tim-icons icon-triangle-right-17 trend-up"></i> +20%</h5>	
          </template>	
          <div class="chart-area">	
            <line-chart style="height: 100%"	
                        chart-id="green-line-chart"	
                        :chart-data="smallYellowLine.chartData"	
                        :gradient-stops="smallYellowLine.gradientStops"	
                        :extra-options="smallYellowLine.extraOptions">	
            </line-chart>	
          </div>	
        </card>
      </div>

      <div class="col-3">
        <card type="chart" class="shorter-cards">	    
          <template slot="header">	
            <h5 class="card-category">Average Length of Stay</h5>	
            <h3 class="card-title">7.5 Days</h3>	
            <h5 class="card-title"><i class="tim-icons icon-triangle-right-17 trend-down"></i> -15%</h5>	
          </template>	
          <div class="chart-area">	
            <line-chart style="height: 100%"	
                        chart-id="purple-line-chart"	
                        :chart-data="smallRedLine.chartData"	
                        :gradient-colors="smallRedLine.gradientColors"	
                        :gradient-stops="smallRedLine.gradientStops"	
                        :extra-options="smallRedLine.extraOptions">	
            </line-chart>	
          </div>	
        </card>
      </div>

      <div class="col-3">
        <card type="chart" class="shorter-cards">	 
          <template slot="header">	
            <h5 class="card-category">Average Admission Cost</h5>	
            <h3 class="card-title">$388,204</h3>	
            <h5 class="card-title"><i class="tim-icons icon-triangle-right-17 trend-down"></i> -1%</h5>	
          </template>	
          <div class="chart-area">	
            <line-chart style="height: 100%"	
                        chart-id="green-line-chart"	
                        :chart-data="smallPinkLine.chartData"	
                        :gradient-stops="smallPinkLine.gradientStops"	
                        :extra-options="smallPinkLine.extraOptions">	
            </line-chart>	
          </div>	
        </card>
      </div>
    </div>

    <!-- STREAM LINE -->
    <div class="row">
      <div class="col-12">
        <card type="chart">
          <template slot="header">
            <div class="row">
              <div class="col-sm-6" :class="isRTL ? 'text-right' : 'text-left'">
                <h5 class="card-category">Departments</h5>
                <h2 class="card-title">Patient Care Score</h2>
              </div>
              <div class="col-sm-6">
                <div class="btn-group btn-group-toggle"
                     :class="isRTL ? 'float-left' : 'float-right'"
                     data-toggle="buttons">
                  <label v-for="(option, index) in bigLineChartCategories"
                         :key="option"
                         class="btn btn-sm btn-primary btn-simple"
                         :class="{active: bigLineChart.activeIndex === index}"
                         :id="index">
                    <input type="radio"
                           @click="initBigChart(index)"
                           name="options" autocomplete="off"
                           :checked="bigLineChart.activeIndex === index">
                    {{option}}
                  </label>
                </div>
              </div>
            </div>
          </template>
          <div class="chart-area">
            <line-chart style="height: 100%"
                        v-if="loaded"
                        ref="bigChart"
                        chart-id="big-line-chart"
                        :chart-data="bigLineChart.chartData"
                        :gradient-colors="bigLineChart.gradientColors"
                        :gradient-stops="bigLineChart.gradientStops"
                        :extra-options="bigLineChart.extraOptions">
            </line-chart>
          </div>
        </card>
      </div>
    </div>

    <!-- OTHER CHARTS -->
    <div class="row">
      <div class="col-lg-4" :class="{'text-right': isRTL}">
        <card type="chart" class="taller-cards">
          <template slot="header">
            <h3 class="card-title"><i class="tim-icons icon-time-alarm text-warning "></i> {{$t('dashboard.dailySales')}}</h3>
          </template>
          <div class="chart-area">
            <bar-chart style="height: 100%"
                       chart-id="blue-bar-chart"
                       :chart-data="blueBarChart.chartData"
                       :gradient-stops="blueBarChart.gradientStops"
                       :extra-options="blueBarChart.extraOptions">
            </bar-chart>
          </div>
        </card>
      </div>
      <div class="col-lg-4" :class="{'text-right': isRTL}">
        <card type="chart" class="taller-cards">
          <template slot="header">
            <h3 class="card-title"><i class="tim-icons icon-puzzle-10 text-primary "></i> {{$t('dashboard.radar')}}</h3>
          </template>
          <div class="chart-area">
            <radar-chart style="height: 100%"
                        chart-id="some-radar-chart"
                        :chart-data="someRadarChart.chartData"
                        :gradient-colors="someRadarChart.gradientColors"
                        :gradient-stops="someRadarChart.gradientStops"
                        :extra-options="someRadarChart.extraOptions">
            </radar-chart>
          </div>
        </card>
      </div>
      <div class="col-lg-4" :class="{'text-right': isRTL}">
        <card type="chart" class="taller-cards">
          <template slot="header">
            <!-- <h5 class="card-category">{{$t('dashboard.polar')}}</h5> -->
            <h3 class="card-title"><i class="tim-icons icon-istanbul text-muted "></i> {{$t('dashboard.polar')}}</h3>
          </template>
          <div class="chart-area">
            <polar-chart style="height: 100%"
                       chart-id="polar-chart"
                       :chart-data="somePolarChart.chartData"
                       :gradient-stops="somePolarChart.gradientStops"
                       :extra-options="somePolarChart.extraOptions">
            </polar-chart>
          </div>
        </card>
      </div>
    </div>



    <!-- MOOOOORE CHARTS -->
    <div class="row">
      <div class="col-lg-4" :class="{'text-right': isRTL}">
        <card type="chart" class="taller-cards">
          <template slot="header">
            <h3 class="card-title"><i class="tim-icons icon-satisfied text-success "></i> {{$t('dashboard.doughnut')}}</h3>
          </template>
          <div class="chart-area">
            <doughnut-chart style="height: 100%"
                       chart-id="some-doughnut-chart"
                       :chart-data="someDoughnutChart.chartData"
                       :gradient-stops="someDoughnutChart.gradientStops"
                       :extra-options="someDoughnutChart.extraOptions">
            </doughnut-chart>
          </div>
        </card>
      </div>
      <div class="col-lg-4" :class="{'text-right': isRTL}">
        <card type="chart" class="taller-cards">
          <template slot="header">
            <h3 class="card-title"><i class="tim-icons icon-badge text-info "></i> {{$t('dashboard.bubble')}}</h3>
          </template>
          <div class="chart-area">
            <bubble-chart style="height: 100%"
                        chart-id="some-bubble-chart"
                        :chart-data="someBubbleChart.chartData"
                        :gradient-colors="someBubbleChart.gradientColors"
                        :gradient-stops="someBubbleChart.gradientStops"
                        :extra-options="someBubbleChart.extraOptions">
            </bubble-chart>
          </div>
        </card>
      </div>
      <div class="col-lg-4" :class="{'text-right': isRTL}">
        <card type="chart" class="taller-cards">
          <template slot="header">
            <h3 class="card-title"><i class="tim-icons icon-single-copy-04 text-danger "></i> {{$t('dashboard.pie')}}</h3>
          </template>
          <div class="chart-area">
            <pie-chart style="height: 100%"
                        chart-id="some-pie-chart"
                        :chart-data="somePieChart.chartData"
                        :gradient-stops="somePieChart.gradientStops"
                        :extra-options="somePieChart.extraOptions">
            </pie-chart>
          </div>
        </card>
      </div>
    </div>


    <!-- BLUE PRINT -->
    <div class="row">
      <div class="col-6">
        <card type="user">
          <template slot="header">
            <div class="row">
              <div class="col-sm-6" :class="isRTL ? 'text-right' : 'text-left'">
                <h5 class="card-category">{{$t('dashboard.campus')}}</h5>
                <h2 class="card-title">{{$t('dashboard.mainLevel')}}</h2>
              </div>
            </div>
          </template>
          <div class="chart-area">

            <img src="img/dpts.png" />
          
          </div>
        </card>
      </div>


      <!-- TASKS -->
      <div class="col-lg-6 col-md-12">
        <card type="tasks" :header-classes="{'text-right': isRTL}">
          <template slot="header">
            <h6 class="title d-inline">{{$t('dashboard.tasks', {count: 10})}}</h6>
            <p class="card-category d-inline">{{$t('dashboard.today')}}</p>
            <base-dropdown menu-on-right=""
                           tag="div"
                           title-classes="btn btn-link btn-icon"
                           aria-label="Settings menu"
                           :class="{'float-left': isRTL}">
              <i slot="title" class="tim-icons icon-settings-gear-63"></i>
              <a class="dropdown-item" href="#pablo">{{$t('dashboard.dropdown.action')}}</a>
              <a class="dropdown-item" href="#pablo">{{$t('dashboard.dropdown.anotherAction')}}</a>
              <a class="dropdown-item" href="#pablo">{{$t('dashboard.dropdown.somethingElse')}}</a>
            </base-dropdown>
          </template>
          <div class="table-full-width table-responsive">
            <task-list></task-list>
          </div>
        </card>
      </div>
    </div>

  </div>
</template>
<script>
  import LineChart from '@/components/Charts/LineChart';
  import BarChart from '@/components/Charts/BarChart';
  import RadarChart from '@/components/Charts/RadarChart';
  import BubbleChart from '@/components/Charts/BubbleChart';
  import ScatterChart from '@/components/Charts/ScatterChart';
  import PolarChart from '@/components/Charts/PolarChart';
  import PieChart from '@/components/Charts/PieChart';
  import DoughnutChart from '@/components/Charts/DoughnutChart';
  import * as chartConfigs from '@/components/Charts/config';
  import TaskList from './Dashboard/TaskList';
  import config from '@/config';
  import UserTable from './Dashboard/UserTable';
  import PatientTable from './Dashboard/PatientTable';
  import axios from 'axios'

  export default {
    components: {
      LineChart,
      BarChart,
      RadarChart,
      BubbleChart,
      ScatterChart,
      PolarChart,
      PieChart,
      DoughnutChart,
      TaskList,
      PatientTable,
      UserTable
    },
    data() {
      return {
        loaded: true,
        stream: null,
        bigLineChart: {
          // index of allData correlates to Department number
          allData: [
            [100, 70, 90, 70, 85, 60, 75, 60, 90, 80, 110, 100],
            [80, 120, 105, 110, 95, 105, 90, 100, 80, 95, 70, 120],
            [60, 80, 65, 130, 80, 105, 90, 130, 70, 115, 60, 130]
          ],
          activeIndex: 0,
          chartData: null,
          extraOptions: chartConfigs.bigLineChartOptions,
          gradientColors: config.colors.primaryGradient,
          gradientStops: [1, 0.4, 0],
          categories: []
        },
        purpleLineChart: {
          extraOptions: chartConfigs.purpleChartOptions,
          chartData: {
            labels: ['JUL', 'AUG', 'SEP', 'OCT', 'NOV', 'DEC'],
            datasets: [{
              label: "Data",
              fill: true,
              borderColor: config.colors.primary,
              borderWidth: 2,
              borderDash: [],
              borderDashOffset: 0.0,
              pointBackgroundColor: config.colors.primary,
              pointBorderColor: 'rgba(255,255,255,0)',
              pointHoverBackgroundColor: config.colors.primary,
              pointBorderWidth: 20,
              pointHoverRadius: 4,
              pointHoverBorderWidth: 15,
              pointRadius: 4,
              data: [80, 100, 70, 80, 120, 80],
            }]
          },
          gradientColors: config.colors.primaryGradient,
          gradientStops: [1, 0.2, 0],
        },
        greenLineChart: {
          extraOptions: chartConfigs.greenChartOptions,
          chartData: {
            labels: ['JUL', 'AUG', 'SEP', 'OCT', 'NOV'],
            datasets: [{
              label: "My First dataset",
              fill: true,
              borderColor: config.colors.danger,
              borderWidth: 2,
              borderDash: [],
              borderDashOffset: 0.0,
              pointBackgroundColor: config.colors.danger,
              pointBorderColor: 'rgba(255,255,255,0)',
              pointHoverBackgroundColor: config.colors.danger,
              pointBorderWidth: 20,
              pointHoverRadius: 4,
              pointHoverBorderWidth: 15,
              pointRadius: 4,
              data: [90, 27, 60, 12, 80],
            }]
          },
          gradientColors: ['rgba(66,134,121,0.15)', 'rgba(66,134,121,0.0)', 'rgba(66,134,121,0)'],
          gradientStops: [1, 0.4, 0],
        },
        smallBlueLine: {
          extraOptions: chartConfigs.smallChartOptions,
          chartData: {
            labels: [],
            datasets: [{
              label: "Data",
              fill: true,
              borderColor: '#11cdef',
              borderWidth: 2,
              borderDash: [],
              borderDashOffset: 0.0,
              pointBackgroundColor: '#11cdef',
              pointBorderColor: 'rgba(255,255,255,0)',
              pointBorderWidth: 20,
              pointRadius: 4,
              data: [80, 100, 70, 80, 120, 80],
            }]
          },
          gradientColors: config.colors.primaryGradient,
          gradientStops: [1, 0.2, 0],
        },
        smallPinkLine: {
          extraOptions: chartConfigs.smallChartOptions,
          chartData: {
            labels: [],
            datasets: [{
              label: "Data",
              fill: true,
              borderColor: '#f3a4b5',
              borderWidth: 2,
              borderDash: [],
              borderDashOffset: 0.0,
              pointBackgroundColor: '#f3a4b5',
              pointBorderColor: 'rgba(255,255,255,0)',
              pointHoverBackgroundColor: '#f3a4b5',
              pointBorderWidth: 20,
              pointHoverRadius: 4,
              pointHoverBorderWidth: 15,
              pointRadius: 4,
              data: [100, 80, 70, 80, 120, 80],
            }]
          },
          gradientColors: config.colors.primaryGradient,
          gradientStops: [1, 0.2, 0],
        },
        smallRedLine: {
          extraOptions: chartConfigs.smallChartOptions,
          chartData: {
            labels: [],
            datasets: [{
              label: "Data",
              fill: true,
              borderColor: '#8965e0',
              borderWidth: 2,
              borderDash: [],
              borderDashOffset: 0.0,
              pointBackgroundColor: '#8965e0',
              pointBorderColor: 'rgba(255,255,255,0)',
              pointHoverBackgroundColor: '#8965e0',
              pointBorderWidth: 20,
              pointHoverRadius: 4,
              pointHoverBorderWidth: 15,
              pointRadius: 4,
              data: [90, 0, 50],
            }]
          },
          gradientColors: config.colors.primaryGradient,
          gradientStops: [1, 0.2, 0],
        },
        smallYellowLine: {
          extraOptions: chartConfigs.smallChartOptions,
          chartData: {
            labels: [],
            datasets: [{
              label: "Data",
              fill: true,
              borderColor: '#ffd600',
              borderWidth: 2,
              borderDash: [],
              borderDashOffset: 0.0,
              pointBackgroundColor: '#ffd600',
              pointBorderColor: 'rgba(255,255,255,0)',
              pointHoverBackgroundColor: '#ffd600',
              pointBorderWidth: 20,
              pointHoverRadius: 4,
              pointHoverBorderWidth: 15,
              pointRadius: 4,
              data: [0, 90, 50],
            }]
          },
          gradientColors: config.colors.primaryGradient,
          gradientStops: [1, 0.2, 0],
        },
        someRadarChart: {
          chartData: {
            labels: [ "SSI",
              "CAUTI",
              "CLABSI",
              "PU",
              "Falls",
              "Sepsis"
            ],
            datasets: [{
              label: "HAC",
              fill: true,
              borderColor: config.colors.primary,
              borderWidth: 2,
              borderDash: [],
              borderDashOffset: 0.0,
              pointBackgroundColor: config.colors.primary,
              pointBorderColor: 'rgba(255,255,255,0)',
              pointHoverBackgroundColor: config.colors.primary,
              pointBorderWidth: 20,
              pointHoverRadius: 4,
              pointHoverBorderWidth: 15,
              pointRadius: 4,
              data: [110, 100, 107, 104, 99, 109],
            },
            ]
          },
          gradientColors: config.colors.primaryGradient,
          gradientStops: [1, 0.2, 0],
        },
        greenRadarChart: {
          chartData: {
            labels: ['JUL', 'AUG', 'SEP', 'OCT', 'NOV'],
            datasets: [{
              label: "My First dataset",
              fill: true,
              borderColor: config.colors.danger,
              borderWidth: 2,
              borderDash: [],
              borderDashOffset: 0.0,
              pointBackgroundColor: config.colors.danger,
              pointBorderColor: 'rgba(255,255,255,0)',
              pointHoverBackgroundColor: config.colors.danger,
              pointBorderWidth: 20,
              pointHoverRadius: 4,
              pointHoverBorderWidth: 15,
              pointRadius: 4,
              data: [90, 27, 60, 12, 80],
            }]
          },
          gradientColors: ['rgba(66,134,121,0.15)', 'rgba(66,134,121,0.0)', 'rgba(66,134,121,0)'],
          gradientStops: [1, 0.4, 0],
        },
        blueRadarChart: {
          // extraOptions: chartConfigs.barChartOptions,
          chartData: {
            labels: ['USA', 'GER', 'AUS', 'UK', 'RO', 'BR'],
            datasets: [{
              label: "Countries",
              fill: true,
              borderColor: config.colors.info,
              borderWidth: 2,
              borderDash: [],
              borderDashOffset: 0.0,
              data: [53, 20, 10, 80, 100, 45],
            }]
          },
          gradientColors: config.colors.primaryGradient,
          gradientStops: [1, 0.4, 0],
        },
        blueBarChart: {
          chartData: {
            labels: ['ER', 'ICU', '2nd Floor', 'Rehab', 'Room', '3rd Floor'],
            datasets: [{
              label: "Departments",
              fill: true,
              borderColor: config.colors.info,
              borderWidth: 2,
              borderDash: [],
              borderDashOffset: 0.0,
              data: [5, 20, 10, 37, 9, 45],
            }]
          },
          gradientColors: config.colors.primaryGradient,
          gradientStops: [1, 0.4, 0],
        },
        someBubbleChart: {
          chartData: {
            labels: ['USA', 'GER', 'AUS', 'UK', 'RO', 'BR'],
            datasets: [{
              label: "Patient Staff Ratio",
              fill: true,
              borderColor: '#11cdef',
              borderDashOffset: 0.0,
              data: [
                {
                  x: 20,
                  y: 20,
                  r: 10,
                }, {
                    x: 2,
                    y: 11,
                    r: 10
                }, {
                    x: 19,
                    y: 19,
                    r: 2
                }, {
                    x: 17,
                    y: 16,
                    r: 4
                }, {
                    x: 15,
                    y: 14,
                    r: 2
                }, {
                    x: 9,
                    y: 7,
                    r: 6
                }, {
                    x: 13,
                    y: 13,
                    r: 5
                }, {
                    x: 11,
                    y: 11,
                    r: 5
                }, {
                    x: 8,
                    y: 8,
                    r: 5
                }, {
                    x: 4,
                    y: 4,
                    r: 19
                }
              ]
            }]
          },
          gradientColors: config.colors.primaryGradient,
          gradientStops: [1, 0.4, 0],
        },
        someDoughnutChart: {
          chartData: {
            labels: ['Very Unsatisfied', 'Unsatisfied', 'Neutral', 'Satisfied', 'Very Satisfied'],
            datasets: [{
              label: "Patient Satisfaction",
              fill: true,
              borderColor: [
                '#f5365c',
                '#ffd600',
                '#2dce89',
                '#5e72e4',
                '#f3a4b5'
                ],
              borderWidth: 2,
              borderDash: [],
              borderDashOffset: 0.0,
              data: [1, 9, 36, 44, 10],
            }]
          },
          gradientColors: config.colors.primaryGradient,
          gradientStops: [1, 0.4, 0],
        },
        somePieChart: {
          // extraOptions: chartConfigs.barChartOptions,
          chartData: {
            labels: ['Humana', 'Kaiser', 'BlueCross', 'Aetna', 'Medicare', 'Medicaid'],
            datasets: [{
              label: "Insurance Provider",
              fill: true,
              borderColor: [
                '#f5365c',
                // '#fb6340',
                '#ffd600',
                // '#2dce89',
                '#5e72e4',
                '#8965e0',
                // '#5603ad',
                '#f3a4b5',
                // '#11cdef',
                '#2bffc6'
                ],
              borderWidth: 2,
              borderDash: [],
              borderDashOffset: 0.0,
              data: [53, 20, 10, 80, 100, 45],
            }]
          },
          gradientColors: config.colors.primaryGradient,
          gradientStops: [1, 0.4, 0],
        },
        somePolarChart: {
          // extraOptions: chartConfigs.barChartOptions,
          chartData: {
            labels: [
              "MICU",
              "SICU",
              "CICU",
              "Neuro/Medical",
              "Ortho/Surgical",
              "Rehab",
              "PCU"
            ],
            datasets: [{
              label: "Countries",
              fill: true,
              borderColor: [
                '#f5365c',
                '#ffd600',
                '#2dce89',
                '#5e72e4',
                '#5603ad',
                '#f3a4b5',
                '#2bffc6'
                ],
              borderWidth: 2,
              data: [53, 20, 10, 80, 100, 45, 110],
            }]
          },
          gradientColors: config.colors.primaryGradient,
          gradientStops: [1, 0.4, 0],
        }
      }
    },
    computed: {
      enableRTL() {
        return this.$route.query.enableRTL;
      },
      isRTL() {
        return this.$rtl.isRTL;
      },
      bigLineChartCategories() {
        return this.$t('dashboard.chartCategories');
      }
    },
    methods: {
      initBigChart(index) {
        let chartData = {
          datasets: [{
            fill: true,
            borderColor: config.colors.primary,
            borderWidth: 2,
            borderDash: [],
            borderDashOffset: 0.0,
            pointBackgroundColor: config.colors.primary,
            pointBorderColor: 'rgba(255,255,255,0)',
            pointHoverBackgroundColor: config.colors.primary,
            pointBorderWidth: 20,
            pointHoverRadius: 4,
            pointHoverBorderWidth: 15,
            pointRadius: 4,
            data: this.bigLineChart.allData[index]
          }]
        }
        // this.$refs.bigChart.updateGradients(chartData);
        this.bigLineChart.chartData = chartData;
        this.bigLineChart.activeIndex = index;
      },
    },
    async mounted () {
      axios.get(`https://pulse-sfmc.herokuapp.com/streams`)
      .then(response => {
        this.stream = response.data.stream.metrics
      })
      .catch(e => {
        this.errors.push(e)
      })

      this.initBigChart(0);
    },
  };
</script>
<style>
</style>
