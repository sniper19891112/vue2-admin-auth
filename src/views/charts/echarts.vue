<template>
    <section class="chart-container">
        <el-row>
            <el-col :span="12">
                <div id="chartColumn" style="width:100%; height:400px;"></div>
            </el-col>
            <el-col :span="12">
                <div id="chartBar" style="width:100%; height:400px;"></div>
            </el-col>
            <el-col :span="12">
                <div id="chartLine" style="width:100%; height:400px;"></div>
            </el-col>
            <el-col :span="12">
                <div id="chartPie" style="width:100%; height:400px;"></div>
            </el-col>
            <el-col :span="24">
                <a href="http://echarts.baidu.com/examples.html" target="_blank" style="float: right;">more>></a>
            </el-col>
        </el-row>
    </section>
</template>

<script>
    import echarts from 'echarts'

    export default {
        data() {
            return {
                chartColumn: null,
                chartBar: null,
                chartLine: null,
                chartPie: null
            }
        },

        methods: {
            drawColumnChart() {
                this.chartColumn = echarts.init(document.getElementById('chartColumn'));
                const option = {
                    title: {text: 'Column Chart'},
                    tooltip: {},
                    xAxis: {
                        data: ["衬衫", "羊毛衫", "雪纺衫", "裤子", "高跟鞋", "袜子"]
                    },
                    yAxis: {},
                    series: [{
                        name: '销量',
                        type: 'bar',
                        data: [5, 20, 36, 10, 10, 20]
                    }],
                    label: {
                        normal: {
                            show: false,
                            position: 'top'
                        }
                    },
                    itemStyle: {
                        normal: {
                            //每个柱子的颜色即为colorList数组里的每一项，如果柱子数目多于colorList的长度，则柱子颜色循环使用该数组
                            color: function (params) {
                                var colorList = ['#4f81bd', '#c0504d', '#9bbb59', '#604a7b', '#948a54', '#e46c0b'];
                                return colorList[params.dataIndex];
                            }
                        }
                    }
                };
                this.chartColumn.setOption(option);
                this.handleChartLoop(option, this.chartColumn);
            },
            drawBarChart() {
                this.chartBar = echarts.init(document.getElementById('chartBar'));
                const option = {
                    title: {
                        text: 'Bar Chart'
                    },
                    tooltip: {
                        trigger: 'axis',
                        axisPointer: {
                            type: 'shadow'
                        }
                    },
                    legend: {
                        data: ['2011年', '2012年']
                    },
                    grid: {
                        left: '3%',
                        right: '4%',
                        bottom: '3%',
                        containLabel: true
                    },
                    xAxis: {
                        type: 'value',
                        boundaryGap: [0, 0.01]
                    },
                    yAxis: {
                        type: 'category',
                        data: ['巴西', '印尼', '美国', '印度', '中国', '世界人口(万)']
                    },
                    label: {
                        normal: {
                            show: true,
                            position: 'right'
                        }
                    },
                    series: [
                        {
                            name: '2011年',
                            type: 'bar',
                            data: [18203, 23489, 29034, 104970, 131744, 630230]
                        },
                        {
                            name: '2012年',
                            type: 'bar',
                            data: [19325, 23438, 31000, 121594, 134141, 681807]
                        }
                    ]
                }
                this.chartBar.setOption(option);
                this.handleChartLoop(option, this.chartBar);
            },
            drawLineChart() {
                this.chartLine = echarts.init(document.getElementById('chartLine'));
                const option = {
                    title: {
                        text: 'Line Chart'
                    },
                    tooltip: {
                        trigger: 'axis'
                    },
                    legend: {
                        data: ['邮件营销', '联盟广告', '搜索引擎']
                    },
                    grid: {
                        left: '3%',
                        right: '4%',
                        bottom: '3%',
                        containLabel: true
                    },
                    xAxis: {
                        type: 'category',
                        boundaryGap: false,
                        data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
                    },
                    label: {
                        normal: {
                            show: true,
                            position: 'top'
                        }
                    },
                    yAxis: {
                        type: 'value'
                    },
                    series: [
                        {
                            name: '邮件营销',
                            type: 'line',
                            stack: '总量',
                            data: [120, 132, 101, 134, 90, 230, 210]
                        },
                        {
                            name: '联盟广告',
                            type: 'line',
                            stack: '总量',
                            data: [220, 182, 191, 234, 290, 330, 310]
                        },
                        {
                            name: '搜索引擎',
                            type: 'line',
                            stack: '总量',
                            data: [820, 932, 901, 934, 1290, 1330, 1320]
                        }
                    ]
                };
                this.chartLine.setOption(option);
                this.handleChartLoop(option, this.chartLine);
            },
            drawPieChart() {
                this.chartPie = echarts.init(document.getElementById('chartPie'));
                const option = {
                    title: {
                        text: 'Pie Chart',
                        subtext: '纯属虚构',
                        x: 'center'
                    },
                    tooltip: {
                        trigger: 'item',
                        formatter: "{a} <br/>{b} : {c} ({d}%)"
                    },
                    legend: {
                        orient: 'vertical',
                        left: 'left',
                        data: ['直接访问', '邮件营销', '联盟广告', '视频广告', '搜索引擎']
                    },
                    label: {
                        normal: {
                            formatter: '{b}:{c}: ({d}%)',
                            textStyle: {
                                fontWeight: 'normal',
                                fontSize: 15
                            }
                        }
                    },
                    // label:{            //饼图图形上的文本标签
                    //     normal:{
                    //         show:true,
                    //         position:'inner', //标签的位置
                    //         textStyle : {
                    //             fontWeight : 300 ,
                    //             fontSize : 16    //文字的字体大小
                    //         },
                    //         formatter:'{d}%'
                    //     }
                    // },
                    series: [
                        {
                            name: '访问来源',
                            type: 'pie',
                            radius: '55%',
                            center: ['50%', '60%'],
                            data: [
                                {value: 335, name: '直接访问'},
                                {value: 310, name: '邮件营销'},
                                {value: 234, name: '联盟广告'},
                                {value: 135, name: '视频广告'},
                                {value: 1548, name: '搜索引擎'}
                            ],
                            itemStyle: {
                                emphasis: {
                                    shadowBlur: 10,
                                    shadowOffsetX: 0,
                                    shadowColor: 'rgba(0, 0, 0, 0.5)'
                                }
                            }
                        }
                    ]
                };
                this.chartPie.setOption(option);
                this.handleChartLoop(option, this.chartPie);
            },
            // 饼图自动轮播
            handleChartLoop: function (option, myChart) {
                if (!myChart) {
                    return
                }
                let currentIndex = -1 // 当前高亮图形在饼图数据中的下标
                let changePieInterval = setInterval(selectPie, 1000) // 设置自动切换高亮图形的定时器

                // 取消所有高亮并高亮当前图形
                function highlightPie() {
                    // 遍历饼图数据，取消所有图形的高亮效果
                    for (let idx in option.series[0].data) {
                        myChart.dispatchAction({
                            type: 'downplay',
                            seriesIndex: 0,
                            dataIndex: idx
                        })
                        // showTip
                        myChart.dispatchAction({
                            type: 'showTip',
                            seriesIndex: 0,
                            dataIndex: idx
                        });
                    }
                    // 高亮当前图形
                    myChart.dispatchAction({
                        type: 'highlight',
                        seriesIndex: 0,
                        dataIndex: currentIndex
                    })
                    // showTip
                    myChart.dispatchAction({
                        type: 'showTip',
                        seriesIndex: 0,
                        dataIndex: currentIndex
                    });
                }

                // 用户鼠标悬浮到某一图形时，停止自动切换并高亮鼠标悬浮的图形
                myChart.on('mouseover', (params) => {
                    clearInterval(changePieInterval)
                    currentIndex = params.dataIndex
                    highlightPie()
                })

                // 用户鼠标移出时，重新开始自动切换
                myChart.on('mouseout', (params) => {
                    if (changePieInterval) {
                        clearInterval(changePieInterval)
                    }
                    changePieInterval = setInterval(selectPie, 1000)
                })

                // 高亮效果切换到下一个图形
                function selectPie() {
                    const dataLen = option.series[0].data.length
                    currentIndex = (currentIndex + 1) % dataLen
                    highlightPie()
                }
            },
            drawCharts() {
                this.drawColumnChart()
                this.drawBarChart()
                this.drawLineChart()
                this.drawPieChart()
            },
        },

        mounted: function () {
            const that = this;
            that.drawCharts();
            window.onresize = function() {
                that.chartColumn.resize();
                that.chartBar.resize();
                that.chartLine.resize();
                that.chartPie.resize();
            };
        },
        updated: function () {
            this.drawCharts()
        },
    }
</script>

<style scoped>
    .chart-container {
        width: 100%;
        float: left;
    }

    /*.chart div {
        height: 400px;
        float: left;
    }*/

    .el-col {
        padding: 30px 20px;
    }
</style>
