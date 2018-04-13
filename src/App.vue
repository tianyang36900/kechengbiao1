<template>
	<div id="app">
		<!--<div class="input">
			<input type="text"  v-model="y.name"/>
			<br />
			<input type="password" v-model="y.passw"/>
			<br />
			<button @click="denglu">登录</button>
			<button @click="zhuce">注册</button>
		</div>-->
		<el-menu :default-active="activeIndex2" class="el-menu-demo" mode="horizontal" @select="handleSelect" background-color="#545c64" text-color="#fff" active-text-color="#ffd04b">
			<!--<el-menu-item index="1">
				<router-link to="/">星期</router-link>
			</el-menu-item>-->
			<el-menu-item index="2">
				<router-link to="/1">星期一</router-link>
			</el-menu-item>
			<el-menu-item index="3">
				<router-link to="/2">星期二</router-link>
			</el-menu-item>
			<el-menu-item index="4">
				<router-link to="/3">星期三</router-link>
			</el-menu-item>
			<el-menu-item index="5">
				<router-link to="/4">星期四</router-link>
			</el-menu-item>
			<el-menu-item index="6">
				<router-link to="/5">星期五</router-link>
			</el-menu-item>
		</el-menu>
		<router-view/>
	</div>
</template>
<script>
	export default {
		create() {
			console.log('111')
			if(this.$route.params.id == null) {
				this.activeIndex2 = "1"
			} else {
				this.activeIndex2 = parseInt(this.$route.params.id) + 1 + ""
			}
		},
		data() {
			return {
				activeIndex2: ""
//				y:{
//					name:"",
//					passw:""
//				}
			};
		},
		methods: {
			handleSelect(key, keyPath) {
				console.log(key, keyPath);
			}
//			denglu(){
//				this.$http.post('http://localhost:8000/land',this.y,{
//					emulateJSON: true}).then(function(e){
//						if (e.body=="2") {
//							
//						} else if(e.body=="1"){
//							alert("账号密码错误")
//						}
//					})
//				}
//				zhuce(){
//				this.$http.post('http://localhost:8000/land',this.y,{
//					emulateJSON: true}).then(function(e){
//						if (e.body=="2") {
//							
//						} else if(e.body=="1"){
//							alert("账号密码错误")
//						}
//					})
//				}
			}
		}
	
</script>
<style>
	#app {
		font-family: 'Avenir', Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		/*text-align: center;*/
		color: #2c3e50;
	}
	
	.el-menu-item {
		padding: 0;
	}
	
	a {
		display: block;
		padding: 0 20px;
		text-decoration: none;
	}
	
	#nav {
		padding: 30px;
	}
	
	#nav a {
		font-weight: bold;
		color: #2c3e50;
	}
	
	#nav a.router-link-exact-active {
		color: #42b983;
	}
</style>