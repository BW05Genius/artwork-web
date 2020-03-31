<template>
	<div class="background">
		<el-form ref="loginForm" :model="form" :rules="rules" label-width="80px" class="login-box">
			<h3 class="login-title">艺术品网站商城</h3>
			<el-form-item label="账号" prop="account">
				<el-input type="text" placeholder="请输入账号" v-model="form.account" />
			</el-form-item>
			<el-form-item label="密码" prop="password">
				<el-input type="password" placeholder="请输入密码" v-model="form.password" />
			</el-form-item>
			<el-form-item label="验证码" prop="code">
				<el-col :span="12">
					<el-input type="text" placeholder="请输入验证码" v-model="form.code" />
				</el-col>
				<span style="display: inline-block;width: 110px;height: 40px;border: 1px solid #D7D7D7;" @click="changeImgCode">
					<img src="http://localhost:43000/user/kaptcha" title="看不清,换一张" style="width: 110px;height:40px;cursor: pointer;" />
				</span>
			</el-form-item>
			<el-form-item>
				<el-button type="primary" v-on:click="onSubmit">登录</el-button>
				<el-button class="button" type="primary" v-on:click="register">去注册</el-button>
			</el-form-item>
		</el-form>

		<el-dialog title="温馨提示" :visible.sync="dialogVisible" width="30%">
			<span>请输入账号和密码</span>
			<span slot="footer" class="dialog-footer">
				<el-button type="primary" @click="dialogVisible = false">确 定</el-button>
			</span>
		</el-dialog>
	</div>
</template>

<script>
	export default {
		name: "Login",
		data() {
			return {
				form: {
					account: '',
					password: '',
					code: ''
				},

				// 表单验证，需要在 el-form-item 元素中增加 prop 属性
				rules: {
					account: [{
						required: true,
						message: '账号不可为空',
						trigger: 'blur'
					}],
					password: [{
						required: true,
						message: '密码不可为空',
						trigger: 'blur'
					}]
				},
				dialogVisible: false,
			}
		},
		methods: {
			onSubmit() {
				this.axios.get("http://localhost:43000/user/checkCode",{
					params:{
						code:this.form.code,
						account:this.form.account,
						password:this.form.password
					}
				}).then(res => {
					console.log(res)
					if (res.data=="1") {
						this.$notify({
							title: '成功',
							message: '恭喜你,登录成功！！！！',
							type: 'success'
						});
						this.$router.push("list");
					} else if(res.data=="2"){
						this.$notify({
							title: '失败',
							message: '抱歉,账户名或密码输入错误！！！！',
							type: 'error'
						});
					}else{
						this.$notify({
							title: '失败',
							message: '抱歉,验证码输入错误！！！！',
							type: 'error'
						});
					}
				})
			},
			register() {
				this.$router.push("/register");
			},
			changeImgCode() {
				window.location.reload();
			},
		}
	}
</script>

<style>
	.login-box {
		border: 1px solid #DCDFE6;
		width: 350px;
		margin: 180px auto;
		padding: 35px 35px 15px 35px;
		border-radius: 5px;
		-webkit-border-radius: 5px;
		-moz-border-radius: 5px;
		box-shadow: 0 0 25px #909399;
		background-image: url("D:\\pic\\artwork\\1.jpg");
	}

	.login-title {
		text-align: center;
		margin: 0 auto 40px 20px;
		color: #303133;
	}

	.button {
		margin-right: 50px
	}

	.background {
		width: 100%;
		height: 100%;
		background-size: cover;
		z-index: -1;
		position: absolute;
		left: 0;
		top: 0;
		background-image: url("D:\\pic\\artwork\\5.jpg");
	}
</style>
