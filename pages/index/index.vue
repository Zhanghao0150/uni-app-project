<template>
	<view class="container">
		<view><text>分享必须要用button 且 属性里面要有 open-type="share" ，uni-app 的api只支持app的分享，小程序的不支持 </text></view>
		<button type="default" open-type="share">分享例子</button>

	</view>
</template>

<script>
	export default {
		data() {
			return {

			}
		},

		onShareAppMessage: function(res) {
			var that = this;
			if (res.from === 'button') {
				console.log('来自页面内转发按钮');
			} else if (res.from === 'menu') {
				console.log('右上角菜单转发按钮');
			}
			// 返回数据
			return {
				title: '我在江湖',
				path: 'pages/share/share',
				imageUrl:'http://slyx.17w.vip/game/static/scrollImage/%E6%88%91%E5%9C%A8%E6%B1%9F%E6%B9%962.jpg',
				success: function(res) {
					// 转发成功，可以把当前页面的链接发送给后端，用于记录当前页面被转发了多少次或其他业务
					wx.request({
						url: app.buildUrl("/member/share"),
						data: {
							url: utils.getCurrentPageUrlWithArgs()
						},
						success: function(res) {
							console.log('分享成功');
						}
					});
				},
				fail: function(res) {
					console.log('分享失败');
				}
			}
		},
		methods: {


		}
	}
</script>

<style>
	.container {
		padding: 20px;
		font-size: 14px;
		line-height: 24px;
	}
</style>
