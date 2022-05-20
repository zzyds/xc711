<template>
	<view class="input-item">
		<view class="input-title">
			<text>{{q.title + "  " + (q.unit?"(" + q.unit + ")":"")}}</text>
		</view>
		<view v-for="(item,index) in q.options" :key="index">
			<view class="input-wraper" :class="q.options.length>1?'muti':''">
				<view class="input-fullwidth">
					<input v-if="q.inputType == 'text'" type="text" :placeholder="item.placeholder"
						placeholder-class="placeholder-style" v-model="q.answer[index]" />
					<input v-else type="number" :placeholder="item.placeholder" placeholder-class="placeholder-style"
						v-model="q.answer[index]" />
				</view>
			</view>

		</view>
	</view>
</template>

<script>
	export default {
		name: "qs-input",
		data() {
			return {

			};
		},
		props: ["q"]
	}
</script>

<style scoped>
	.uni-input-input {
		width: 100%;
	}

	.input-item {

		margin: 40rpx 0;
	}

	.input-title {
		font-size: 30rpx;
		font-weight: 400;
		color: #FFFFFF;
		line-height: 36rpx;
		margin-left: 16rpx;
		margin-bottom: 12rpx;
	}

	.input-wraper {
		background-image: url('https://xc-evaluation.oss-cn-hangzhou.aliyuncs.com/ds/quick_review2.0/images/questions/input.png');

		background-size: 517rpx 65rpx;
		background-repeat: no-repeat;
		background-position: left top;
		height: 65rpx;
		/* border: 2rpx solid #499EED; */

		font-size: 24rpx;
		font-family: "PingFang SC";
		font-weight: 400;
		color: #DADADA;

		line-height: 65rpx;
		text-align: left;
		padding: 0 30rpx;

		display: flex;
		align-items: center;
	}

	.input-wraper.muti {
		margin: 16rpx 0;
	}

	.input-fullwidth {
		flex: 1;
	}

	.placeholder-style {
		font-size: 24rpx;
		font-family: "PingFang SC";
		font-weight: 400;
		color: #DADADA;
		line-height: 36rpx;
	}
</style>
