<template>
	<view class=""
		@touchstart="handleTouchStart"
		@touchend="handleTouchEnd">
		学习触屏事件
	</view>
</template>

<script>
	/*
		1.给容器绑定触屏事件 touchstart touchend
		2.按下屏幕时
			1.记录按下屏幕的时间 Date.now() 时间戳 返回1970-1-1至今的毫秒数
			2.记录按下屏幕的坐标 x 和 y
		3.离开屏幕事件
			1.记录离开屏幕的时间 Date.now() 
			2.记录离开屏幕的坐标 x 和 y
			3.根据两个时间 运算 判断 按下屏幕时长是否合法
			4.根据两对坐标 判断距离是否合法 判断滑动的方向
	*/
	export default {
		data() {
			return {
				// 按下的时间
				startTime: 0,
				// 按下的坐标
				startX: 0,
				startY: 0
			}
		},
		methods: {
			// 按下屏幕
			handleTouchStart(event) {
				this.startTime = Date.now();
				this.startX = event.changedTouches[0].clientX;
				this.startY = event.changedTouches[0].clientY;
			},
			
			// 离开屏幕
			handleTouchEnd(event) {
				const endTime = Date.now();
				const endX = event.changedTouches[0].clientX;
				const endY = event.changedTouches[0].clientY;
				
				// 判断按下的时长
				if(endTime - this.startTime > 2000) {
					return;
				}
				
				// 滑动方向
				let direction = "";
				
				// 判断滑动距离是否合法 判断滑动方向
				if(Math.abs(endX - this.startX) > 10) {
					// 滑动方向
					direction = endX - this.startX > 0 ? "right":"left";
				} else {
					return;
				}
				
				console.log(direction);
			}
		}
	}
</script>

<style>
	view {
		width: 100%;
		height: 500rpx;
		background-color: #007AFF;
	}
</style>
