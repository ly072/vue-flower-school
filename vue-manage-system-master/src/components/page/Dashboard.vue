<template>
	<div>
		<el-row :gutter="20">
			<el-col :span="8">
				<el-card shadow="hover" class="mgb20" style="height:252px;">
					<div class="user-info">
						<img src="../../assets/img/img.jpg" class="user-avator" alt />
						<div class="user-info-cont">
							<div class="user-info-name">{{name}}</div>
							<div>{{role}}</div>
						</div>
					</div>
					<div class="user-info-list">
						上次登录时间：
						<span>2020-4-25</span>
					</div>
					<div class="user-info-list">
						上次登录地点：
						<span>漳州</span>
					</div>
				</el-card>
				<el-card shadow="hover" style="height:740px;">
					<div slot="header" class="clearfix">
						<span>AP详情</span>
					</div>
					蓝钟花<el-progress :percentage="21.6" color="#42b983"></el-progress>
					毛茛<el-progress :percentage="67.1" color="#f1e05a"></el-progress>
					款冬<el-progress :percentage="82.2"></el-progress>
					樱草<el-progress :percentage="89.9" color="#f56c6c"></el-progress>
					藏红花<el-progress :percentage="84.9" color="#FFB6C1"></el-progress>
					黄水仙<el-progress :percentage="40.3" color="#FFC0CB"></el-progress>
					雏菊<el-progress :percentage="84.7" color="#DB7093"></el-progress>
					蒲公英<el-progress :percentage="93.9" color="#FF69B4"></el-progress>
					贝母<el-progress :percentage="68.6" color="#DA70D6"></el-progress>
					鸢尾花<el-progress :percentage="96.3" color="#DDA0DD"></el-progress>
					铃兰<el-progress :percentage="65.8" color="#EE82EE"></el-progress>
					兰色紫罗兰<el-progress :percentage="69.9" color="#FF00FF"></el-progress>
					雪花莲<el-progress :percentage="84.1" color="#7FFFAA"></el-progress>
					向日葵<el-progress :percentage="95.1" color="#7CFC00"></el-progress>
					虎百合<el-progress :percentage="68.3" color="#B22222"></el-progress>
					郁金香<el-progress :percentage="74.1" color="#CD853F"></el-progress>
					银莲花<el-progress :percentage="65.1" color="#FFFF00"></el-progress>

				</el-card>
			</el-col>
			<el-col :span="16">
				<el-row :gutter="20" class="mgb20">
					<el-col :span="8">
						<el-card shadow="hover" :body-style="{padding: '0px'}">
							<div class="grid-content grid-con-1">
								<i class="el-icon-lx-people grid-con-icon"></i>
								<div class="grid-cont-right">
									<div class="grid-num">1234</div>
									<div>用户访问量</div>
								</div>
							</div>
						</el-card>
					</el-col>
					<el-col :span="8">
						<el-card shadow="hover" :body-style="{padding: '0px'}">
							<div class="grid-content grid-con-2">
								<i class="el-icon-lx-notice grid-con-icon"></i>
								<div class="grid-cont-right">
									<div class="grid-num">321</div>
									<div>系统消息</div>
								</div>
							</div>
						</el-card>
					</el-col>
					<el-col :span="8">
						<el-card shadow="hover" :body-style="{padding: '0px'}">
							<div class="grid-content grid-con-3">
								<i class="el-icon-lx-goods grid-con-icon"></i>
								<div class="grid-cont-right">
									<div class="grid-num">5000</div>
									<div>预测数量</div>
								</div>
							</div>
						</el-card>
					</el-col>
				</el-row>

				<el-card shadow="hover" style="height:403px;">
					<div slot="header" class="clearfix">
						<span>每日一花</span>
						<el-button @click="handleEditDailyForm" style="float: right; padding: 3px 0" type="text">添加</el-button>
					</div>
					<el-table :data="todoList1" style="width:100%;" max-height="300">
						<el-table-column label="题目">
							<template slot-scope="scope">
								<span>{{scope.row.title}}</span>
							</template>
						</el-table-column>
						<!-- :filters="[{ text: '未发布', value: '未发布' }, { text: '已发布', value: '已发布' }]" -->
						<el-table-column label="发布状态">
							<template slot-scope="scope">
								<el-tag :type="scope.row.status === 'false' ? 'primary' : 'success'" disable-transitions>{{scope.row.status=="false"?'未发布':'已发布'}}</el-tag>
							</template>
						</el-table-column>
						<el-table-column label="发布时间">
							<template slot-scope="scope">
								<span>{{scope.row.date}}</span>
							</template>
						</el-table-column>
						<el-table-column label="操作" width="120">
							<template slot-scope="scope">
								<el-button type="text" icon="el-icon-edit" @click="editDailyForm(scope.$index, scope.row)" :disabled="scope.row.status === 'false' ? false : true">编辑</el-button>

								<el-button type="text" icon="el-icon-delete" class="red" @click="handleDeleteDaily(scope.$index,scope.row)"
								 :disabled="scope.row.status === 'false' ? false : true">删除</el-button>
							</template>
						</el-table-column>
					</el-table>
				</el-card>
				<br />

				<el-card shadow="hover" style="height:470px;">
					<div slot="header" class="clearfix">
						<span>每日推荐</span>
						<el-button style="float: right; padding: 3px 0" type="text" @click="handleEditCommandForm">添加</el-button>
					</div>
					<el-table :data="todoList2" style="width:100%;">
						<el-table-column label="内容">
							<template slot-scope="scope">
								<div class="todo-item">{{scope.row.content}}</div>
							</template>
						</el-table-column>
						<el-table-column label="发布状态">
							<template slot-scope="scope">
								<el-tag :type="scope.row.status === 'false' ? 'primary' : 'success'" disable-transitions>
									{{scope.row.status=="false"?'未发布':'已发布'}}
								</el-tag>
							</template>
						</el-table-column>
						<el-table-column label="发布时间" prop="date">
							<!-- 							<template slot-scope="scope">
								<span>{{scope.row.date}}</span>
							</template> -->
						</el-table-column>
						<el-table-column label="操作" width="120">
							<template slot-scope="scope">
								<el-button type="text" icon="el-icon-edit" @click="editCommandForm(scope.$index, scope.row)" :disabled="scope.row.status === 'false' ? false : true">编辑</el-button>

								<el-button type="text" icon="el-icon-delete" class="red" @click="handleDeleteCommand(scope.$index,scope.row)"
								 :disabled="scope.row.status === 'false' ? false : true">删除</el-button>
							</template>
						</el-table-column>
					</el-table>
				</el-card>
			</el-col>
		</el-row>
		<!-- 每日推荐编辑弹出框 -->
		<el-dialog title="每日推荐" :visible.sync="editCommandVisible">
			<el-form :rules="commandRules" ref="commandForm" :model="commandForm" label-width="70px">
				<el-form-item label="内容" required prop="content">
					<el-input type="textarea" autosize placeholder="请输入内容" v-model="commandForm.content">
					</el-input>
				</el-form-item>
				<el-form-item label="文件" required prop="fileList">
					<el-upload class="upload-demo" action="https://jsonplaceholder.typicode.com/posts/" :http-request="commandUpload"
					 :on-preview="handlePreview" :on-remove="handleRemove" :file-list="commandForm.fileList" list-type="picture">
						<el-button size="small" type="primary">点击上传</el-button>
						<div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div>
					</el-upload>
				</el-form-item>
				<el-form-item label="发布时间" required prop="date">
					<el-col :span="11">
						<el-date-picker :picker-options="pickerOptions0" v-model="commandForm.date" type="date" placeholder="选择日期" format="yyyy 年 MM 月 dd 日"
						 value-format="yyyy-MM-dd">
						</el-date-picker>
					</el-col>
				</el-form-item>
				</el-form-item>
			</el-form>
			<span slot="footer" class="dialog-footer">
				<el-button @click="editCommandVisible = false">取 消</el-button>
				<el-button type="primary" @click="handleSaveCommandForm('commandForm')">确 定</el-button>
			</span>
		</el-dialog>
		<!-- 每日一花编辑弹出框 -->
		<el-dialog title="每日一花" :visible.sync="editDailyVisible">
			<el-form :rules="rules" ref="dailyForm" :model="dailyForm" label-width="70px">
				<el-form-item label="题目" required prop="title">
					<el-input v-model="dailyForm.title"></el-input>
				</el-form-item>
				<el-form-item label="文件" required prop="fileList">
					<el-upload class="upload-demo" action="https://jsonplaceholder.typicode.com/posts/" :http-request="modeUpload"
					 :on-preview="handlePreview" :on-remove="handleRemove" :file-list="dailyForm.fileList" list-type="picture">
						<el-button size="small" type="primary">点击上传</el-button>
						<div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div>
					</el-upload>
				</el-form-item>
				<el-form-item label="选项一" required prop="option1">
					<el-input v-model="dailyForm.option1"></el-input>
				</el-form-item>
				<el-form-item label="选项二" required prop="option2">
					<el-input v-model="dailyForm.option2"></el-input>
				</el-form-item>
				<el-form-item label="发布时间" required prop="date">
					<el-col :span="11">
						<el-date-picker :picker-options="pickerOptions0" v-model="dailyForm.date" type="date" placeholder="选择日期" format="yyyy 年 MM 月 dd 日"
						 value-format="yyyy-MM-dd">
						</el-date-picker>
					</el-col>
				</el-form-item>
				</el-form-item>
				<el-form-item label="答案" prop="answer">
					<el-select v-model="dailyForm.answer" placeholder="请选择答案">
						<el-option :label="dailyForm.option1" :value="dailyForm.option1"></el-option>
						<el-option :label="dailyForm.option2" :value="dailyForm.option2"></el-option>
					</el-select>
				</el-form-item>
			</el-form>
			<span slot="footer" class="dialog-footer">
				<el-button @click="editDailyVisible = false">取 消</el-button>
				<el-button type="primary" @click="saveEdit('dailyForm')">确 定</el-button>
			</span>
		</el-dialog>
	</div>
</template>

<script>
	import Schart from 'vue-schart';
	import bus from '../common/bus';
	export default {
		name: 'dashboard',
		data() {
			return {
				pickerOptions0: {
					disabledDate(time) {
						return time.getTime() < Date.now(); //如果没有后面的-8.64e6就是不可以选择今天的
					}
				},
				//-8.64e6
				value: '',
				upfile: {},
				fileList: [],
				editDailyVisible: false,
				editCommandVisible: false,
				dailyForm: {
					title: '',
					option1: '',
					option2: '',
					option: [{
						value: '',
						label: ''
					}, {
						value: '',
						label: ''
					}],
					answer: '',
					date: '',
					fileList: [],
					status: false
				},
				commandForm: {
					content: '',
					date: '',
					fileList: [],
				},
				commandRules: {
					content: [{
						required: true,
						message: '请输入推荐内容',
						trigger: 'blur'
					}, ],
					date: [{
						required: true,
						message: '请选择日期'
					}],
					fileList: [{
						required: true,
						message: '请选择文件',
						trigger: 'change'
					}]
				},
				rules: {
					title: [{
						required: true,
						message: '请输入题目',
						trigger: 'blur'
					}, ],
					option1: [{
						required: true,
						message: '请输入选项',
						trigger: 'change'
					}],
					option2: [{
						required: true,
						message: '请输入选项',
						trigger: 'change'
					}],
					fileList: [{
						required: true,
						message: '请选择文件',
						trigger: 'change'
					}],
					answer: [{
						required: true,
						message: '请选择答案',
						trigger: 'change'
					}]
				},
				date1: '',
				file: '',
				URL_DEFINE_ROOT: 'http://localhost/flower/fl/admin',
				name: localStorage.getItem('ms_username'),
				todoList1: [{
						title: '蒲公英',
						status: false
					},
					{
						title: '雏菊',
						status: false
					}
				],

				todoList2: [{
						title: '推荐一',
						status: false
					},
					{
						title: '推荐二',
						status: false
					}
				],
				ip: returnCitySN['cip'],
				cityname: returnCitySN['cname']
			};
		},
		components: {
			Schart
		},
		created() {
			this.getDailyFlowerList();
			this.getDailyCommandList();
		},
		computed: {
			role() {
				return this.name === 'admin' ? '超级管理员' : '普通用户';
			}
		},
		// created() {
		//     this.handleListener();
		//     this.changeDate();
		// },
		// activated() {
		//     this.handleListener();
		// },
		// deactivated() {
		//     window.removeEventListener('resize', this.renderChart);
		//     bus.$off('collapse', this.handleBus);
		// },
		methods: {
			dateFormat: function(row, column) {
				var date = row[column.property];
				if (date === undefined) {
					return ''
				};
				return moment(date).format("YYYY-MM-DD")
			},
			commandUpload: function(item) {
				this.upfile = item.file;
				// console.log("?????",this.commandForm.fileList);
				this.commandForm.fileList = true;
			},
			modeUpload: function(item) {
				// console.log(item.file);
				this.upfile = item.file;
				this.dailyForm.fileList = true;
			},
			submitUpload: function() {
				this.$refs.upload.submit();
			},
			handleRemove: function(file, fileList) {
				console.log(file, fileList);
			},
			handlePreview: function(file) {
				console.log(file);
			},
			editDailyForm: function(index, row) {
				this.dailyForm = row;
				console.log('e’', row);
				this.dailyForm.fileList = [{
					name: row.fileList,
					url: this.URL_DEFINE_ROOT + '/dailyFlower/' + row.filename
				}];
				this.handleEditDailyForm();
			},
			handleEditCommandForm: function() {
				this.editCommandVisible = true;
			},
			editCommandForm: function(index, row) {
				this.commandForm = row;
				console.log('e’', row);
				this.commandForm.fileList = [{
					name: row.fileList,
					url: this.URL_DEFINE_ROOT + '/dailyCommand/' + row.filename
				}];
				this.editCommandVisible = true;
			},
			handleDeleteCommand: function(index, row) {
				// 二次确认删除
				this.$confirm('确定要删除吗？', '提示', {
					type: 'warning'
				}).then(() => {
					let data = new FormData();
					var adminId = sessionStorage.getItem('adminId');
					data.append('adminId', adminId);
					data.append('commandId', row.commandId);
					console.log('commandId', row.commandId);
					this.$axios.post(this.URL_DEFINE_ROOT + '/delDailyCommand.php', data).then((res) => {
						if (res.data.status == 'success') {
							console.log('success');
							this.$message.success('删除成功');
							// this.tableData.splice(index, 1);
							this.getDailyCommandList();
						} else {
							console.log('error');
							return false;
						}
					}).catch((err) => {
						console.log('error');
						console.log(err);
					})
				}).catch(() => {});
			},
			handleSaveCommandForm: function(formName) {
				this.$refs[formName].validate((valid) => {
					if (valid) {
						var adminId = sessionStorage.getItem('adminId')
						let data = new FormData();
						data.append("file", this.upfile);
						data.append('content', this.commandForm['content']);
						data.append('date', this.commandForm['date']);
						data.append('adminId', adminId);
						console.log(data);
						this.$confirm('确定保存吗？', '提示', {
								type: 'warning'
							}).then(() => {
								this.$axios.post(this.URL_DEFINE_ROOT + '/insertDailyCommand.php', data, {
									headers: {
										'Content-Type': 'multipart/form-data'
									}
								}).then((res) => {
									if (res.data.status == 'success') {
										console.log('success');
										this.editCommandVisible = false;
										this.getDailyCommandList();
										this.$message.success('保存成功');
									} else {
										console.log('error');
										this.$message.error('保存失败1');
										return false;
									}
								}).catch((err) => {
									console.log('error');
									this.$message.error('保存失败2');
									console.log(err);
								})

								// this.tableData.splice(index, 1);
							})
							.catch(() => {});
						this.editVisible = false;
						// this.$set(this.tableData, this.idx, this.form);
					} else {
						console.log('error submit!!');
						return false;
					}
				});
			},
			getDailyCommandList: function() {
				let data = new FormData();
				var adminId = sessionStorage.getItem('adminId');
				data.append('adminId', adminId);
				console.log(adminId);
				this.$axios.post(this.URL_DEFINE_ROOT + '/selectDailyCommand.php', data).then((res) => {
					if (res.data.status == 'success') {
						console.log('success');
						this.todoList2 = res.data.data;
						console.log(this.todoList2);
					} else {
						console.log('error');
						return false;
					}
				}).catch((err) => {
					console.log('error');
					console.log(err);
				})
			},
			getDailyFlowerList: function() {
				let data = new FormData();
				var adminId = sessionStorage.getItem('adminId');
				data.append('adminId', adminId);
				console.log("adminId", adminId);
				this.$axios.post(this.URL_DEFINE_ROOT + '/selectDailyFlower.php', data).then((res) => {
					if (res.data.status == 'success') {
						console.log('success');
						this.todoList1 = res.data.data;
						console.log(this.todoList1);
					} else {
						console.log('error');
						return false;
					}
				}).catch((err) => {
					console.log('error');
					console.log(err);
				})
			},
			saveEdit: function(formName) {
				this.$refs[formName].validate((valid) => {
					if (valid) {
						var adminId = sessionStorage.getItem('adminId')
						let data = new FormData();
						data.append("file", this.upfile);
						data.append('title', this.dailyForm['title']);
						data.append('option1', this.dailyForm['option1']);
						data.append('option2', this.dailyForm['option2']);
						data.append('answer', this.dailyForm['answer']);
						data.append('date', this.dailyForm['date']);
						data.append('adminId', adminId);
						this.$confirm('确定保存吗？', '提示', {
								type: 'warning'
							}).then(() => {

								this.$axios.post(this.URL_DEFINE_ROOT + '/insertDailyFlower.php', data, {
									headers: {
										'Content-Type': 'multipart/form-data'
									}
								}).then((res) => {
									if (res.data.status == 'success') {
										console.log('success');
										this.$message.success('保存成功');
										this.editDailyVisible = false;
										this.getDailyFlowerList();
									} else {
										console.log('error');
										this.$message.error('保存失败1');
										return false;
									}
								}).catch((err) => {
									console.log('error');
									this.$message.error('保存失败2');
									console.log(err);
								})

								// this.tableData.splice(index, 1);
							})
							.catch(() => {});
						this.editVisible = false;
						// this.$set(this.tableData, this.idx, this.form);
					} else {
						console.log('error submit!!');
						return false;
					}
				});

			},
			changeDate() {
				const now = new Date().getTime();
				this.data.forEach((item, index) => {
					const date = new Date(now - (6 - index) * 86400000);
					item.name = `${date.getFullYear()}/${date.getMonth() + 1}/${date.getDate()}`;
				});
			},
			// gotoBasForm(){
			//  
			//           //点击跳转至上次浏览页面
			//          // this.$router.go(-1)
			//  
			//           //指定跳转地址
			// 	this.$router.replace('/form')
			// },
			gotoEditor() {
				this.$router.replace('/editor')
			},
			handleEditDailyForm: function() {
				this.editDailyVisible = true;
			},
			handleDelete: function(index, row) {
				// 二次确认删除
				this.$confirm('确定要删除吗？', '提示', {
						type: 'warning'
					})
					.then(() => {
						this.$message.success('删除成功');
						this.tableData.splice(index, 1);
					})
					.catch(() => {});
			},
			// 删除操作
			handleDeleteDaily: function(index, row) {
				// 二次确认删除
				this.$confirm('确定要删除吗？', '提示', {
					type: 'warning'
				}).then(() => {
					let data = new FormData();
					var adminId = sessionStorage.getItem('adminId');
					data.append('adminId', adminId);
					data.append('dailyId', row.dailyId);
					console.log('dailyId', row.dailyId);
					this.$axios.post(this.URL_DEFINE_ROOT + '/delDailyFlower.php', data).then((res) => {
						if (res.data.status == 'success') {
							console.log('success');
							this.$message.success('删除成功');
							// this.tableData.splice(index, 1);
							this.getDailyFlowerList();
						} else {
							console.log('error');
							return false;
						}
					}).catch((err) => {
						console.log('error');
						console.log(err);
					})
				}).catch(() => {});
			},

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

	.ui-upload {
		font-size: 14px;
		width: 80px;
		height: 30px;
		line-height: 30px;
		text-align: center;
		position: relative;
		cursor: pointer;
		color: #fff;
		background: #00abff;
		border-radius: 3px;
		overflow: hidden;
		display: inline-block;
		text-decoration: none;
	}

	.ui-upload input {
		position: absolute;
		font-size: 100px;
		right: 0;
		top: 0;
		opacity: 0;
		filter: alpha(opacity=0);
		cursor: pointer;
	}
</style>
