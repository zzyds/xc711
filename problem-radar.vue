<template>
	<view>
		<view id="myradar"></view>
	</view>
</template>

<script>
	import * as echarts from 'echarts'

	export default {
		name: "problem-radar",
		props: ["fxbgs"],
		data() {
			return {
				bgs: []
			};
		},
		watch: {
			fxbgs() {
				this.bgs = this.fxbgs
				console.log(this.bgs)
				this.getRadar()
			}
		},
		methods: {
			getRadar() {
				let color1 = new echarts.graphic.LinearGradient(1, 0, 0, 0, [{
					offset: 0,
					color: "rgba(0,236,214,1)"
				}, {
					offset: 1,
					color: "rgba(1,162,248,1)"
				}], false)

				let option1 = {
					title: {
						text: '基础雷达图'
					},
					tooltip: {},
					legend: {

						bottom: 5,
						data: ['A', 'B']
					},

					radar: {
						// shape: 'circle',
						name: {
							textStyle: {
								color: '#fff',
								backgroundColor: '#999',
								borderRadius: 3,
								padding: [3, 5]
							}
						},
						splitNumber: 5,

						splitArea: {
							areaStyle: {
								color: ['#591422',
									'#7e5920',
									'#ffc971',
									'#82c0cc',
									'#097c22'
								],
								shadowColor: 'rgba(0, 0, 0, 0.3)',
								shadowBlur: 10
							}
						},
						indicator: [{
								name: '方向1',
								max: 100
							},
							{
								name: '方向2',
								max: 100
							},
							{
								name: '方向3',
								max: 100
							},
							{
								name: '方向4',
								max: 100
							},
							{
								name: '方向5',
								max: 100
							},
							{
								name: '方向6',
								max: 100
							}
						]
					},
					series: [{
						type: 'radar',
						// areaStyle: {normal: {}},
						lineStyle: {
							width: 3,
							color: 'rgba(0,0,0,1)'
						},
						data: [{
								value: [70, 63, 80, 60, 50, 60],
								name: 'A'
							},
							{
								value: [43, 53, 70, 70, 70, 90],
								name: 'B',
								lineStyle: {
									type: 'dashed'
								}
							}

						]
					}]
				};

				let indiColor = ["#92D6FD", "#F3041E","#FF9600","blue","yellow"] //["#F3041E","#FF9600","#92D6FD","#92D6FD","#92D6FD"]
				let indicator = []
				let seriesdata = []
				this.bgs.map((bg, index) => {
					let indi = {}
					indi.name = bg.name
					indi.max = 100 // bg.percent>50? 100 :50
					indi.color = indiColor[index]

					indicator.push(indi)

					seriesdata.push(bg.percent)
				})

				var chartDom = document.getElementById('myradar');
				var myChart = echarts.init(chartDom);
				var option;

				option = {
					title: {
						text: '分析报告雷达图',
						show: false
					},
					legend: {
						data: ['分析报告雷达图1']
					},
					radar: {
						radius: '50%',
						// shape: 'circle',
						//四周文字样式
						nameGap: 5,

						name: {
							// // 在文本中，可以对部分文本采用 rich 中定义样式。
							// // 这里需要在文本中使用标记符号：
							// // `{styleName|text content text content}` 标记样式名。
							// // 注意，换行仍是使用 '\n'。
							// formatter: [
							// 	'{a|流量问题}',
							// 	'{b|这段文本采用样式b}这段用默认样式{x|这段用样式x}'
							// ].join('\n'),

							// rich: {
							// 	a: {
							// 		color: 'green',
							// 		lineHeight: 10
							// 	},
							// 	b: {
							// 		backgroundColor: {
							// 			image: 'https://xc-evaluation.oss-cn-hangzhou.aliyuncs.com/ds/quick_review2.0/images/alpha/lang.png'
							// 		},
							// 		height: 5,
							// 		paddingBottom:30
							// 	},
							// 	x: {
							// 		fontSize: 18,
							// 		fontFamily: 'Microsoft YaHei',
							// 		borderColor: '#449933',
							// 		borderRadius: 4
							// 	},
							// }
							// formater: '{value +"222"}',
							textStyle: {
								color: '#ffc971',
								// backgroundColor: {
								// 	image: 'https://xc-evaluation.oss-cn-hangzhou.aliyuncs.com/ds/quick_review2.0/images/alpha/lang.png',
								// 	size:[80,5],
								// height: 5,
								// },
								borderRadius: 3,
								padding: [3, 5,3,5]
							}
						},
						// splitNumber: 2,

						// 网格线中间区域
						splitArea: {
							areaStyle: {
								color: "rgba(244,23,25,0)",
								shadowColor: 'rgba(0, 0, 0, 0.3)',
								shadowBlur: 10
							},
						},

						// 网格线横竖
						splitLine: {
							show: true,
							lineStyle: {
								width: 1,
								color: 'rgba(68,240,233,.35)', // 设置网格线的颜色
							},
						},
						axisLine: {
							lineStyle: {
								color: 'rgba(68,240,233,.35)',
							},
						},
						indicator: indicator
					},
					series: [{
						name: '分析报告',
						type: 'radar',
						symbolSize: 5, // 拐点的大小
						itemStyle: {
							emphasis: {
								// color: 各异,
								lineStyle: {
									width: 4
								}
							}
						},
						areaStyle: {
							normal: {
								width: 1,
								opacity: 0.5,
								color: color1
							},
						},
						lineStyle: {
							width: 1.5,
							color: '#44f0e9'
						},
						data: [{
							value: seriesdata,
							name: '分析报告雷达图 2'
						}]
					}]
				};

				let option2 = {
					title: {
						text: 'Basic Radar Chart'
					},
					legend: {
						data: ['Allocated Budget', 'Actual Spending']
					},
					radar: {
						radius: '50%',
						// shape: 'circle',
						indicator: [{
								name: 'Sales',
								max: 6500
							},
							{
								name: 'Administration',
								max: 16000
							},
							{
								name: 'Information Technology',
								max: 30000
							},
							{
								name: 'Customer Support',
								max: 38000
							},
							{
								name: 'Development',
								max: 52000
							},
							{
								name: 'Marketing',
								max: 25000
							}
						]
					},
					series: [{
						name: 'Budget vs spending',
						type: 'radar',
						data: [{
								value: [4200, 3000, 20000, 35000, 50000, 18000],
								name: 'Allocated Budget'
							},
							{
								value: [5000, 14000, 28000, 26000, 42000, 21000],
								name: 'Actual Spending'
							}
						]
					}]
				};

				option && myChart.setOption(option);

			}
		},
		mounted() {
			this.bgs = this.fxbgs
			this.getRadar()
		}
	}
</script>

<style>
	#myradar {
		width: 700rpx;
		height: 600rpx;
	}
</style>
