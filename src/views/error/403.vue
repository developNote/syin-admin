<template>
	<div class="content-container">		
		<div class="error-page" id="error-403">
			<div class="pag-container">
				<div class="error-img"></div>
				<div class="error-info">
					<h1 class="error-title">403</h1>
					<p class="error-desc">
						{{tipMsg}}
					</p>

					<el-button type="primary" @click="getback">返回主页</el-button>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import commonMixin from "@/mixins/common";

export default {
	name: "error_403",
	mixins: [commonMixin],
	props: {
		msg: {
			type: String,
		}
	},
  	data() {
		return {
			def_msg: '抱歉，你无权访问该页面',
			tip_msg: '',
		}
	},
	methods: {
		getback(){
			// 返回首页, 此处须知首页的信息
			let router = this.$store.getters['access/routers'][0];

			if(router.hasOwnProperty('children') && router.children.length){
				router = router.children[0];
			}

			// 跳转到首页
			this.$router.push({path: router.path})
		}
	},
	computed: {
		tipMsg(){
			let tip_msg = this.msg;

			if(!tip_msg){
				tip_msg = this.def_msg;
			}

			return tip_msg;
		},
	}
};
</script>

<style lang="scss" scoped>
@import "@/assets/style/error-page.scss";

#error-403{
	.error-img{
		background-image: url("../../assets/img/403.svg");
	}
}
</style>