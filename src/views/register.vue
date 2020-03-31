<template>
	<div align="middle" class="background">
		<el-form ref="form" :model="form" :rules="rules" label-width="80px" class="login-box">
			<h3 class="login-title">用户注册</h3>
			<el-form-item label="账号" prop="username">
				<el-input type="text" placeholder="请输入账号" v-model="form.username" />
			</el-form-item>
			<el-form-item label="密码" prop="password">
				<el-input type="password" placeholder="请输入密码" v-model="form.password" />
			</el-form-item>
			<el-form-item>
				<el-button class="button" type="primary" v-on:click="register">注册</el-button>
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
					username: '',
					password: ''
				},

				// 表单验证，需要在 el-form-item 元素中增加 prop 属性
				rules: {
					username: [{
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

				// 对话框显示和隐藏
				dialogVisible: false
			}
		},
		methods: {
			register() {
				// 为表单绑定验证功能
				this.$confirm('注册成功, 跳转到登录页面?', '提示', {
					confirmButtonText: '确定',
				}).then(() => {
					this.$router.push("/");
					this.$notify({
						title: '成功',
						message: '跳转成功!',
						type: 'success'
					});
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.login-box {
		border: 1px solid #DCDFE6;
		width: 350px;
		margin: 180px auto;
		padding: 35px 35px 15px 35px;
		border-radius: 5px;
		-webkit-border-radius: 5px;
		-moz-border-radius: 5px;
		background-image: url("D:\\pic\\artwork\\1.jpg");
		box-shadow: 0 0 25px #909399;
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
		left: 0;top: 0;
		background-image: url("D:\\pic\\artwork\\5.jpg");
	}
</style>
