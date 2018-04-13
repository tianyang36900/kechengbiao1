<template>
	<div class="home">
		<el-dialog title="新增" :visible.sync="dialogFormVisible">
			<el-form :model="form">
				<!--<el-form-item label="第几节" :label-width="formLabelWidth" >
					<el-input v-model="form.name" auto-complete="off" placeholder="第一节"></el-input>
				</el-form-item>-->
				<el-form-item label="第几节" :label-width="formLabelWidth">
					<el-select v-model="form.name" placeholder="请选择节课">
						<el-option label="第一节" value="第一节"></el-option>
						<el-option label="第二节" value="第二节"></el-option>
						<el-option label="第三节" value="第三节"></el-option>
						<el-option label="第四节" value="第四节"></el-option>
						<el-option label="第五节" value="第五节"></el-option>
						<el-option label="第六节" value="第六节"></el-option>
						<el-option label="第七节" value="第七节"></el-option>
						<el-option label="第八节" value="第八节"></el-option>
					</el-select>
				</el-form-item>
				<el-form-item label="科目" :label-width="formLabelWidth">
					<el-select v-model="form.max" placeholder="请选择科目">
						<el-option label="语文" value="语文"></el-option>
						<el-option label="数学" value="数学"></el-option>
						<el-option label="英语" value="英语"></el-option>
						<el-option label="历史" value="历史"></el-option>
						<el-option label="地理" value="地理"></el-option>
						<el-option label="政治" value="政治"></el-option>
						<el-option label="体育" value="体育"></el-option>
						<el-option label="自习" value="自习"></el-option>
					</el-select>
				</el-form-item>
			</el-form>
			<div slot="footer" class="dialog-footer">
				<el-button @click="dialogFormVisible = false">取 消</el-button>
				<el-button type="primary" @click="submit">确 定</el-button>
			</div>
		</el-dialog>

		<el-button type="success" round @click="dialogFormVisible=true" v-if='$route.params.id=="1"'>+</el-button>

		<el-table :data="tableData" style="width: 100%">
			<!--<el-table-column prop="id" label="日期" width="180">-->
			<!--</el-table-column>-->
			<el-table-column prop="name" label="节课" width="180">
			</el-table-column>
			<el-table-column prop="max" label="科目">

			</el-table-column>
			<el-table-column label="操作">
				<template slot-scope="scope">
					<el-button size="mini" type="danger" icon="el-icon-delete" round @click="handleDelete(scope.row)"></el-button>
					<el-button size="mini" type="danger" @click="daichongxiu(scope.row)">星期二</el-button>
					<el-button size="mini" type="danger" @click="yichongxiu(scope.row)">星期三</el-button>
					<el-button size="mini" type="danger" @click="xingqisi(scope.row)">星期四</el-button>
					<el-button size="mini" type="danger" @click="xingqiwu(scope.row)">星期五</el-button>
				</template>
			</el-table-column>

		</el-table>

	</div>
</template>

<script>
	export default {
		data() {
			return {
				tableData: [],
				dialogFormVisible: false,

				form: {
					name: "",
					max: ""
				},
				formLabelWidth: "120px"
			}
		},
		watch: {
			'$route': function() {
				this.tian()
			}

		},
		created() {
			this.tian()
		},
		methods: {
			submit() {
				this.dialogFormVisible = false,
					this.$http.post('http://localhost:8000/add', this.form, {emulateJSON: true}).then(function() {
						this.tian()
						this.form = {}
						this.$message({
							message: '恭喜你，这是一条成功的消息',
							type: 'success'
						});
					})
			},
			tian: function() {
				this.$http.post('http://localhost:8000', {
					leibie: this.$route.params.id
				}, {
					emulateJSON: true
				}).then((e) => {
					return this.tableData = e.body
				})
			},
			handleDelete(e) {
				this.$http.post('http://localhost:8000/del', {
					id: e.id
				}, {
					emulateJSON: true
				}).then((e) => {
					return e.id = e.body

				})
				var xy = this.tableData.indexOf(e)
				this.tableData.splice(xy, 1)
				this.$message({
					message: '删除成功',
					type: 'success'
				});
			},
			daichongxiu(e) {
				this.$http.post("http://localhost:8000/upate", {
					id: e.id,
					leibie: 2
				}, {
					emulateJSON: true
				}).then(e => {
					this.tian()
					this.$message({
						message: '已转入星期二的课程',
						type: 'success'
					});
				})
			},
			yichongxiu(e) {
				this.$http.post("http://localhost:8000/upate", {
					id: e.id,
					leibie: 3
				}, {
					emulateJSON: true
				}).then(e => {
					this.tian()
					this.$message({
						message: '已转入星期三的课程',
						type: 'success'
					});
				})
			},
			xingqisi(e) {
				this.$http.post("http://localhost:8000/upate", {
					id: e.id,
					leibie: 4
				}, {
					emulateJSON: true
				}).then(e => {
					this.tian()
					this.$message({
						message: '已转入星期四的课程',
						type: 'success'
					});
				})
			},
			xingqiwu(e) {
				this.$http.post("http://localhost:8000/upate", {
					id: e.id,
					leibie: 5
				}, {
					emulateJSON: true
				}).then(e => {
					this.tian()
					this.$message({
						message: '已转入星期五的课程',
						type: 'success'
					});
				})
			}

		}
	}
</script>