<template>
	<div class="common-layout">
		<el-container>
			<el-header class="header">
				<div class="l">🤗 推个免免</div>
				<div class="r">
					<el-link :underline="false" href="https://github.com/KairuiLiu/let-us-baoyan">GitHub</el-link>
				</div>
			</el-header>
			<el-main><FormPage></FormPage></el-main>
			<el-footer>冲天香阵透长安, 满城尽带黄金甲 </el-footer>
		</el-container>
	</div>
</template>

<script setup lang="ts">
import { defineComponent } from 'vue';
import FormPage from './FormPage/index.vue';
</script>

<script lang="ts">
export default defineComponent({
	name: 'IndexPage',
});
</script>

<style lang="less" scoped>
.config {
	width: 10vw;
	min-width: 380px;
}
.common-layout .el-header,
.common-layout .el-footer {
	background-color: #b3c0d1;
	color: var(--el-text-color-primary);
	text-align: center;
	line-height: 60px;
}
.common-layout .el-main {
	background-color: #e9eef3;
	color: var(--el-text-color-primary);
	min-height: calc(100vh - 60px);
	overflow-x: hidden;
}

.header {
	font-size: 20px;
	// text-align: left !important;
	justify-content: space-between;
	display: flex;
}
</style>
