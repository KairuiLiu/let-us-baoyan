<template>
	<div id="form-wapper" :style="{ width: `${infoWidth}%` }">
		<div class="titlebar">
			<span class="title">志愿信息</span>
		</div>
		<div class="info">
			<div class="row">
				<div class="l">层次</div>
				<div class="r"><input class="text-input" type="text" value="Master" /></div>
			</div>
			<div class="row">
				<div class="l">单位</div>
				<div class="r"><input class="text-input" type="text" value="Colleges in Home University(CMU)" /></div>
			</div>
			<div class="row">
				<div class="l">院系</div>
				<div class="r"><input class="text-input" type="text" value="St. Chi College" /></div>
			</div>
			<div class="row">
				<div class="l">专业</div>
				<div class="r"><input class="text-input" type="text" value="Lie Flat（114514）" /></div>
			</div>
			<div class="row">
				<div class="l">学习方式</div>
				<div class="r"><input class="text-input" type="text" value="Self learning" /></div>
			</div>
			<div class="row">
				<div class="l">研究方向</div>
				<div class="r"><input class="text-input" type="text" value="Sell Vegetable" /></div>
			</div>
			<div class="row">
				<div class="l">导师</div>
				<div class="r"><input class="text-input" type="text" value="KevinZonda" /></div>
			</div>
			<div class="row">
				<div class="l">专项计划类型</div>
				<div class="r"><input class="text-input" type="text" value="非专项计划" /></div>
			</div>
			<div class="row">
				<div class="l">就业类型</div>
				<div class="r"><input class="text-input" type="text" value="非定向就业" /></div>
			</div>
		</div>
		<div class="titlebar">
			<span class="title yellow">待录取通知</span>
			<span class="note">&nbsp;&nbsp;接受或拒绝待录取通知后，将无法更改。</span>
		</div>
		<div class="info">
			<div class="note"><input class="text-input" type="text" value="Colleges in Home University 招生办 2022-09-31 00:00" /></div>
			<div class="blueball">
				您已被拟录取，请尽快确认。
				<div class="result">
					<div class="result-box" :class="state">
						<span class="icon"
							><el-icon v-if="state === 'accept'"><CircleCheckFilled /></el-icon>
							<el-icon v-else><CircleCloseFilled /></el-icon>
						</span>
						<span> <input v-model="textRes" class="text-input" type="text" :style="{ width: mirror?.offsetWidth ? `${mirror.offsetWidth + 4}px` : 'unset' }" /> </span>
					</div>
				</div>
			</div>
		</div>
	</div>

	<br />
	<br />

	<div id="control">
		<p>浅灰色部分及录取结果都能改</p>
		<el-form-item label="宽度">
			<el-slider v-model="infoWidth" />
		</el-form-item>
		<el-form-item label="状态">
			<el-radio-group v-model="state">
				<el-radio-button label="accept"
					><el-icon><CircleCheckFilled /></el-icon>接受</el-radio-button
				>
				<el-radio-button label="reject"
					><el-icon><CircleCloseFilled /></el-icon>拒绝</el-radio-button
				>
			</el-radio-group>
		</el-form-item>
		<el-form-item label="操作">
			<el-button type="primary" @click="toImg()">截图</el-button>
		</el-form-item>
	</div>
	<div class="zero-height-box">
		<div ref="mirror" class="result-box" :class="state">
			<span> {{ textRes }} </span>
		</div>
	</div>
</template>

<script setup lang="ts">
import domtoimage from 'dom-to-image';
import { defineComponent, ref } from 'vue';
import { CircleCheckFilled, CircleCloseFilled } from '@element-plus/icons-vue';

const infoWidth = ref(100);
const state = ref('accept');
const textRes = ref('您于9月31日 00:01接受了 Colleges in Home University 的录取通知');
const mirror = ref();
function toImg() {
	const node = document.getElementById('form-wapper');
	domtoimage.toPng(node).then((dataUrl: string) => {
		const a = document.createElement('a');
		const event = new MouseEvent('click');
		a.download = '推个免免';
		a.href = dataUrl; // 将生成的URL设置为a.href属性
		a.dispatchEvent(event); // 触发a的单击事件
	});
}
</script>

<script lang="ts">
export default defineComponent({
	name: 'FormPage',
});
</script>

<style lang="less" scoped>
#form-wapper {
	position: relative;
	left: 50%;
	transform: translateX(-50%);
	// min-width: 640px;
	// max-width: 70vw;
	border: 1px solid #cacaca;
	.titlebar {
		position: relative;
		padding: 8px;
		background-color: #f9f9f9;
		border: solid #cacaca;
		border-width: 1px 0;
		&:first-of-type {
			border-width: 0 0 1px;
		}

		.title {
			color: #5ba8b7;
			font-weight: bold;
			&.yellow {
				color: #c89c3b;
			}
		}
	}
	.info {
		position: relative;
		padding: 8px;
		background-color: #fff;
		.row {
			display: flex;
			.l {
				color: #7c7c7c;
				line-height: 2;
				width: 40%;
				text-align: right;
				font-weight: bold;
				&::after {
					content: ':';
					margin-right: 8px;
				}
			}
			.r {
				color: #787878;
				line-height: 2;
				width: 60%;
			}
		}
	}
	.note {
		color: #89878c;
	}
	.blueball {
		&::before {
			content: '';
			display: block;
			width: 15px;
			height: 15px;
			position: absolute;
			border: #c3dae2 solid;
			border-width: 1px 1px 0 0;
			background-color: #e3f2f9;
			transform: rotateZ(-45deg);
			top: -8.5px;
			left: 29px;
		}
		position: relative;
		border: 1px #c3dae2 solid;
		background-color: #e3f2f9;
		padding: 8px;
		width: calc(100% - 64px);
		margin: 20px auto;
		color: #3e454d;
		.result {
			margin: 16px auto;
			display: flex;
			justify-content: center;
			.result-box {
				padding: 8px 16px;
				font-weight: bold;
				color: green;
				&.reject {
					color: red;
				}
				background-color: #ccc;
				display: flex;
				span {
					&.icon {
						font-size: 1.2rem;
						line-height: 2;
					}
					line-height: 16px;
					font-size: 16px;
					vertical-align: middle;
				}
			}
		}
	}
}

.zero-height-box {
	// height: 0;
	// visibility: hidden;
	display: flex;
	justify-content: center;
	.result-box {
		padding: 8px 16px;
		font-weight: bold;
		color: green;
		&.reject {
			color: red;
		}
		background-color: #ccc;
		display: flex;
		span {
			&.icon {
				font-size: 1.2rem;
				line-height: 2;
			}
			line-height: 16px;
			font-size: 16px;
			vertical-align: middle;
		}
	}
}

#control {
	width: 30vw;
	min-width: 320px;
}

.text-input {
	outline: none;
	border-style: none;
	appearance: none;
	background-color: #0000;
	color: inherit;
	width: 100%;
	line-height: 2;
	font-size: 16px;
	font-weight: inherit;
}

.zero-height-box {
	height: 0;
	visibility: hidden;
	overflow: hidden;
	position: fixed;
	left: -9999999999px;
	padding: 8px 16px;
	font-weight: bold;
	color: green;
	&.reject {
		color: red;
	}
	background-color: #ccc;
	display: flex;
	span {
		&.icon {
			font-size: 1.2rem;
			line-height: 2;
		}
		line-height: 16px;
		font-size: 16px;
		vertical-align: middle;
	}
}

.slider-demo-block {
	display: flex;
	align-items: center;
}
.slider-demo-block .el-slider {
	margin-top: 0;
	margin-left: 12px;
}
.slider-demo-block .demonstration {
	font-size: 14px;
	color: var(--el-text-color-secondary);
	line-height: 44px;
	flex: 1;
	overflow: hidden;
	text-overflow: ellipsis;
	white-space: nowrap;
	margin-bottom: 0;
}
.slider-demo-block .demonstration + .el-slider {
	flex: 0 0 70%;
}
</style>
