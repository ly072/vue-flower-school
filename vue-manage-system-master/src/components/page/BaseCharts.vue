<template>
	<div align="center">
		<div class="crumbs">
			<el-breadcrumb separator="/">
				<el-breadcrumb-item>
					<i class="el-icon-pie-chart"></i> 数据分析
				</el-breadcrumb-item>
			</el-breadcrumb>
		</div>
		<div>
			<el-row :gutter="20">
				<el-col :span="24">
					<el-card shadow="hover">
						<div id="monthChart" :style="{ height: '300px'}"></div>
					</el-card>
				</el-col>
			</el-row>
			</br>
			<el-row :gutter="20">
				<el-col :span="12">
					<el-card shadow="hover">
						<div id="sexChart" :style="{ height: '300px'}"></div>
					</el-card>
				</el-col>
				<el-col :span="12">
					<el-card shadow="hover">
						<div id="frequencyChart" :style="{ height: '300px'}"></div>
					</el-card>
				</el-col>
			</el-row>
			<el-row :gutter="20">
				<el-col :span="24">
					<el-card shadow="hover">
						<div id="myChartChina" :style="{width: '100%', height: '500px'}"></div>
					</el-card>
				</el-col>
			</el-row>
		</div>
	</div>
</template>

<script>
	import Schart from 'vue-schart';
	import bus from '../common/bus';
	export default {
		name: 'dashboard',
		data() {
			return {
				// name: localStorage.getItem('ms_username'),
				monthOptions: {
					title: {
						text: '最近一月份用户预测花朵次数条形图',
						left: 'center'
					},
					tooltip: {},
					toolbox: {
						show: true,
						right: '50',
						feature: {
							dataZoom: {
								yAxisIndex: 'none'
							},
							dataView: {readOnly: false},
							saveAsImage: {}
						}
					},
					xAxis: {
						data: ['蓝钟', '花毛', '茛款', '冬樱草', '藏红花', '黄水仙', '雏菊', '蒲公英', '贝母', '鸢尾花', '铃兰', '兰色紫罗兰', '雪花莲', '向日葵', '虎百合', '郁金香',
							'银莲花', 'Unknow'
						],
						axisTick: {
							alignWithLabel: true
						},
						axisLabel: {
							interval: 0,
							rotate: 40
						}
					},
					yAxis: {
						type: 'value'
					},
					series: [{
						name: '数量',
						type: 'bar',
						data: [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
					}]
				},
				sexOptions: {
					
					title: {
						text: '用户男女比例',
						left: 'center'
					},
					toolbox: {
						show: true,
						feature: {
							dataView: {readOnly: false},
							saveAsImage: {}
						}
					},
					tooltip:{},
					legend: {
						orient: 'vertical',

						left: 10,
						data: ['男', '女', '未知']
					},
					bgColor: '#fbfbfb',
					series: [{
						name: '用户男女比例',
						type: 'pie',
						radius: '55%',
						data: [{
								value: 235,
								name: '男'
							},
							{
								value: 274,
								name: '女'
							},
							{
								value: 274,
								name: '未知'
							},
						]
					}]
				},
				mapOptions:{
					title: {
						text: '用户地域分布图',
						left: 'center'
					},
					tooltip: {
						trigger: 'item',
						showDelay: 0,
						transitionDuration: 0.2,
						formatter: function(params) {
							var value = (params.value + '').split('.');
							value = value[0].replace(/(\d{1,3})(?=(?:\d{3})+(?!\d))/g, '$1,');
							return params.seriesName + '<br/>' + params.name + ': ' + value;
						}
					},
					legend: {
						orient: 'vertical',
						left: '10',
						data: ['']
					},
					visualMap: {
						min: 0,
						max: 1500,
						left: 'left',
						top: 'bottom',
						text: ['高', '低'],
						calculable: true,
						inRange: {
							color: ['lightskyblue', 'yellow', 'orangered']
						}
					},
					selectedMode: 'single',
					toolbox: {
						show: true,
						//orient: 'vertical',
						top: 'top',
						feature: {
							dataView: {
								readOnly: false
							},
							restore: {},
							saveAsImage: {}
						}
					},
					series: [{
						name: '中国',
						type: 'map',
						roam: true,
						mapType: 'china',
						itemStyle: {
							normal: {
								borderColor: 'rgba(0, 0, 0, 0.2)'
							},
							emphasis: {
								shadowOffsetX: 0,
								shadowOffsetY: 0,
								shadowBlur: 20,
								borderWidth: 0,
								shadowColor: 'rgba(0, 0, 0, 0.5)'
							}
						},
						showLegendSymbol: true,
						label: {
							normal: {
								show: true
							},
							emphasis: {
								show: true
							}
						},
						data: [{
								name: '北京',
								value: 1
							},
							{
								name: '天津',
								value: 1
							},
							{
								name: '上海',
								value: 1
							},
							{
								name: '重庆',
								value: 1
							},
							{
								name: '河北',
								value: 400
							},
							{
								name: '河南',
								value: 275
							},
							{
								name: '云南',
								value: 643
							},
							{
								name: '辽宁',
								value: 963
							},
							{
								name: '黑龙江',
								value: 342
							},
							{
								name: '湖南',
								value: 132
							},
							{
								name: '安徽',
								value: 54
							},
							{
								name: '山东',
								value: 767
							},
							{
								name: '新疆',
								value: 14
							},
							{
								name: '江苏',
								value: 546
							},
							{
								name: '浙江',
								value: 432
							},
							{
								name: '江西',
								value: 43
							},
							{
								name: '湖北',
								value: 321
							},
							{
								name: '广西',
								value: 43
							},
							{
								name: '甘肃',
								value: 32
							},
							{
								name: '山西',
								value: 534
							},
							{
								name: '内蒙古',
								value: 321
							},
							{
								name: '陕西',
								value: 435
							},
							{
								name: '吉林',
								value: 98
							},
							{
								name: '福建',
								value: 765
							},
							{
								name: '贵州',
								value: 45
							},
							{
								name: '广东',
								value: 765
							},
							{
								name: '青海',
								value:22
							},
							{
								name: '西藏',
								value: 242
							},
							{
								name: '四川',
								value: 342
							},
							{
								name: '宁夏',
								value: 234
							},
							{
								name: '海南',
								value: 54
							},
							{
								name: '台湾',
								value: 643
							},
							{
								name: '香港',
								value: 543
							},
							{
								name: '澳门',
								value: 54
							}
						]
					}]
				},
				frequencyOptions:{
					title:{
						text:'最近一周用户登录频率情况',
						left:'left'
					},
					tooltip:{
						trigger: 'axis'
					},
					toolbox: {
						show: true,
						feature: {
							dataView: {readOnly: false},
							magicType: {type: ['line', 'bar']},
							restore: {},
							saveAsImage: {}
						}
					},
					xAxis: {
						type: 'category',
						boundaryGap: false,
						data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
					},
					yAxis: {
						type: 'value'
					},
					series: [{
						data: [0, 0, 0, 0, 0, 0, 0],
						type: 'line',
						markPoint: {
							data: [
								{type: 'max', name: '最大值'},
								{type: 'min', name: '最小值'}
							]
						},
						// areaStyle: {}
					}]
				},
				URL_DEFINE_ROOT: 'http://localhost/flower/fl/admin'
			};
		},
		created() {
			this.getMonthIdentificationData();
			this.getData();
			this.getFrequencyData();
			this.getMapData();
		},
		mounted() {
			this.drawLine();
			this.drawLine2();
			this.drawLine3();
			this.drawLine4();
		},
		components: {
			Schart
		},

		methods: {
			drawLine() {
				// 基于准备好的dom，初始化echarts实例
				// var myChartContainer = document.getElementById('monthChart'); 
				let myChart = this.$echarts.init(document.getElementById('monthChart'), 'light');
				// 绘制图表
				myChart.setOption(this.monthOptions);
			},
			drawLine2() {
				let myChart = this.$echarts.init(document.getElementById('sexChart'), 'light')
				// 绘制图表
				myChart.setOption(this.sexOptions);
			},
			drawLine4() {
				let myChart = this.$echarts.init(document.getElementById('frequencyChart'), 'light')
				// 绘制图表
				myChart.setOption(this.frequencyOptions);
			},
			getData: function() {
				let data = new FormData();
				var adminId = sessionStorage.getItem('adminId');
				data.append('adminId', adminId);
				this.$axios.post(this.URL_DEFINE_ROOT + '/calUserBySex.php', data).then((res) => {
					console.log("??",res.data);
					if (res.data.status == 'success') {
						console.log('success');
						this.$message.success('获取成功');
						// this.tableData.splice(index, 1);
						this.sexOptions.series[0]['data'] = [{
							value: Number(res.data.data[0]['男']),
							name: '男'
						}, {
							value: Number(res.data.data[0]['女']),
							name: '女'
						}, {
							value: Number(res.data.data[0]['未知']),
							name: '未知'
						}, ]
						this.drawLine2();
					} else {
						console.log('error');
						return false;
					}
				}).catch((err) => {
					console.log('error');
					console.log(err);
				})
			},
			drawLine3() {
				// 基于准备好的dom，初始化echarts实例
				console.log('domsada');
				var myChart = this.$echarts.init(document.getElementById('myChartChina'));
				function randomData() {
					return Math.round(Math.random() * 500);
				}
				// 绘制图表
				myChart.showLoading();
				myChart.hideLoading();
				myChart.setOption(this.mapOptions);
			},
			getMapData: function() {
				let data = new FormData();
				var adminId = sessionStorage.getItem('adminId');
				data.append('adminId', adminId);
				this.$axios.post(this.URL_DEFINE_ROOT + '/calMapData.php', data).then((res) => {
					console.log(res);
					console.log(res.data);
					console.log(res.data.data);
					console.log(res.data.status);
					if (res.data.status == 'success') {
						console.log('success');
						this.$message.success('获取成功');
						// this.tableData.splice(index, 1);
						// var data1 = res.data.data;
						this.mapOptions.series.data=res.data.data
						this.drawLine4();
					} else {
						console.log('error');
						return false;
					}
				}).catch((err) => {
					console.log('error');
					console.log(err);
				})
			},
			getFrequencyData: function() {
				let data = new FormData();
				var adminId = sessionStorage.getItem('adminId');
				data.append('adminId', adminId);
				this.$axios.post(this.URL_DEFINE_ROOT + '/calFrequency.php', data).then((res) => {
					if (res.data.status == 'success') {
						console.log('success');
						this.$message.success('获取成功');
						// this.tableData.splice(index, 1);
						var data1 = res.data.data[0];
						var num = data1[""+i];
						if (num != undefined){
							this.frequencyOptions.series[0]['data'][6] = Number(num);
						}
						// var labels = this.monthOptions.xAxis['data'];
						for (var i = 1; i < 7; i++) {
							num = data1[""+i];
							if (num == undefined) continue;
							this.frequencyOptions.series[0]['data'][i-1] = Number(num);
							// console.log(labels[i],":",num,this.options1.datasets[0]['data'][i]);
						}
						this.drawLine4();
					} else {
						console.log('error');
						return false;
					}
				}).catch((err) => {
					console.log('error');
					console.log(err);
				})
			},
			getMonthIdentificationData: function() {
				let data = new FormData();
				var adminId = sessionStorage.getItem('adminId');
				data.append('adminId', adminId);
				this.$axios.post(this.URL_DEFINE_ROOT + '/calMonthFlowerIndentification.php', data).then((res) => {
					if (res.data.status == 'success') {
						console.log('success');
						this.$message.success('获取成功');
						// this.tableData.splice(index, 1);
						var data1 = res.data.data[0];
						var labels = this.monthOptions.xAxis['data'];
						for (var i = 0; i <= labels.length; i++) {
							var num = data1[labels[i]];
							if (num == undefined) continue;
							this.monthOptions.series[0]['data'][i] = Number(num);
							// console.log(labels[i],":",num,this.options1.datasets[0]['data'][i]);
						}
						this.drawLine();
					} else {
						console.log('error');
						return false;
					}
				}).catch((err) => {
					console.log('error');
					console.log(err);
				})
			},
			changeDate() {
				const now = new Date().getTime();
				this.data.forEach((item, index) => {
					const date = new Date(now - (6 - index) * 86400000);
					item.name = `${date.getFullYear()}/${date.getMonth() + 1}/${date.getDate()}`;
				});
			}

		}
	};
</script>


<style scoped>
	.el-row {
		margin-bottom: 20px;
	}

	.grid-content {
		display: flex;
		align-items: center;
		height: 100px;
	}

	.grid-cont-right {
		flex: 1;
		text-align: center;
		font-size: 14px;
		color: #999;
	}

	.grid-num {
		font-size: 30px;
		font-weight: bold;
	}

	.grid-con-icon {
		font-size: 50px;
		width: 100px;
		height: 100px;
		text-align: center;
		line-height: 100px;
		color: #fff;
	}

	.grid-con-1 .grid-con-icon {
		background: rgb(45, 140, 240);
	}

	.grid-con-1 .grid-num {
		color: rgb(45, 140, 240);
	}

	.grid-con-2 .grid-con-icon {
		background: rgb(100, 213, 114);
	}

	.grid-con-2 .grid-num {
		color: rgb(45, 140, 240);
	}

	.grid-con-3 .grid-con-icon {
		background: rgb(242, 94, 67);
	}

	.grid-con-3 .grid-num {
		color: rgb(242, 94, 67);
	}

	.user-info {
		display: flex;
		align-items: center;
		padding-bottom: 20px;
		border-bottom: 2px solid #ccc;
		margin-bottom: 20px;
	}

	.user-avator {
		width: 120px;
		height: 120px;
		border-radius: 50%;
	}

	.user-info-cont {
		padding-left: 50px;
		flex: 1;
		font-size: 14px;
		color: #999;
	}

	.user-info-cont div:first-child {
		font-size: 30px;
		color: #222;
	}

	.user-info-list {
		font-size: 14px;
		color: #999;
		line-height: 25px;
	}

	.user-info-list span {
		margin-left: 70px;
	}

	.mgb20 {
		margin-bottom: 20px;
	}

	.todo-item {
		font-size: 14px;
	}

	.todo-item-del {
		text-decoration: line-through;
		color: #999;
	}

	.schart {
		width: 100%;
		height: 300px;
	}
</style>
