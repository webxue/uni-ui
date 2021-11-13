<template>
	<view>
		<uni-popup type="bottom" ref="sharePop" :maskClick="true" @change=change>
			<view class="pop_bg">
				<text class="title">分享至</text>
				<view class="content-share">
					<view v-show="hasWx" class="share_01" @click="share_wx">
						<image src="/static/images/share_wx.png" mode=""></image>
						<text>微信</text>
					</view>
					<view v-show="hasWx" class="share_01" @click="share_wx_q">
						<image src="/static/images/share_wxq.png" mode=""></image>
						<text>朋友圈</text>
					</view>
					<view v-show="hasQQ" class="share_01" @click="share_qq">
						<image src="/static/images/share_qq.png" mode=""></image>
						<text>QQ</text>
					</view>
					<view class="share_01" @click="share_gengduo">
						<image src="/static/images/share_gengduo.png" mode=""></image>
						<text>更多</text>
					</view>
				</view>
				<view class="close_pop" @click="close">
					<text>取消</text>
				</view>
			</view>
		</uni-popup>
	</view>
</template>

<script>
	import {mapGetters} from 'vuex';
	import UniPopup from '@/components/uni-popup/uni-popup.vue'
	export default {
		name: 'AppSharePop',
		components: {
			UniPopup
		},
		data() {
			return {
      };
		},
		props: {
			showpop: {
				type: Boolean,
				default: false
			},
			share_title: {
				type: String,
				default: ''
			},
			share_des: {
				type: String,
				default: ''
			},
			shareUrl: {
				type: String,
				default: ''
			},
			logo_path: {
				type: String,
				default: ''
			},
			//share_type == 2 时为图片分享
			share_type: {
				type: Number,
				default: 0
			}
		},
		watch: {
			showpop(n, o) {
				if (n) {
					this.$refs.sharePop.open()
				} else {
					this.$refs.sharePop.close()
				}
			}
		},
		computed: {
			...mapGetters(['hasQQ','hasWx'])
			// getWx() {
			// 	if (plus.runtime.isApplicationExist({
			// 			pname: 'com.tencent.mm',
			// 			action: 'weixin://'
			// 		})) {
			// 		return true
			// 	} else {
			// 		return false
			// 	}
			// },
			// getQQ() {
			// 	if (plus.runtime.isApplicationExist({
			// 			pname: 'com.tencent.mobileqq',
			// 			action: 'mqq://'
			// 		})) {
			// 		return true
			// 	} else {
			// 		return false
			// 	}
			// }
		},
		methods: {
			close() {
				this.$emit('close')
			},
      change(e) {
        if(!e.show){
          this.$emit('close')
        }
      },
			share_wx() {
				if (this.share_type == 0) {
					uni.share({
						provider: "weixin",
						scene: "WXSceneSession",
						type: 0,
						title: this.share_title,
						summary: this.share_des,
						href: this.shareUrl,
						imageUrl: this.logo_path,
						success: function(res) {
							console.log("success:" + JSON.stringify(res));
						},
						fail: function(err) {
							console.log("fail:" + JSON.stringify(err));
						},
            complete: res => {
              this.$refs.sharePop.close()
            }
					});
				} else {
					uni.share({
						provider: "weixin",
						scene: "WXSceneSession",
						type: 2,
						imageUrl: this.logo_path,
						success: function(res) {
							console.log("success:" + JSON.stringify(res));

						},
						fail: function(err) {
							console.log("fail:" + JSON.stringify(err));
						},
            complete: res => {
              this.$refs.sharePop.close()
            }
					});
				}
			},
			share_wx_q() {
				// this.$emit('wxqchange')
				if (this.share_type == 0) {
					uni.share({
						provider: "weixin",
						scene: "WXSenceTimeline",
						type: 0,
						title: this.share_title,
						summary: this.share_des,
						href: this.shareUrl,
						imageUrl: this.logo_path,
						success: function(res) {
							console.log("success:" + JSON.stringify(res));
						},
						fail: function(err) {
							console.log("fail:" + JSON.stringify(err));
						},
            complete: res => {
              this.$refs.sharePop.close()
            }
					});
				} else {
					uni.share({
						provider: "weixin",
						scene: "WXSenceTimeline",
						type: 2,
						imageUrl: this.logo_path,
						success: function(res) {
							console.log("success:" + JSON.stringify(res));

						},
						fail: function(err) {
							console.log("fail:" + JSON.stringify(err));
						},
            complete: res => {
              this.$refs.sharePop.close()
            }
					});
				}
			},
			share_qq() {
				if (this.share_type == 0) {
          let summary = this.share_title + '\n' + this.share_des + '\n\n' + this.shareUrl
					uni.share({
						provider: "qq",
						type: 1,
            title: this.share_title,
            href: this.shareUrl,
						summary: summary,
						success: function(res) {
							console.log("success:" + JSON.stringify(res));
						},
						fail: function(err) {
							console.log("fail:" + JSON.stringify(err));
						},
            complete: res => {
              this.$refs.sharePop.close()
            }
					});
				} else {
					uni.share({
						provider: "qq",
						type: 2,
						imageUrl: this.logo_path,
						success: function(res) {
							console.log("success:" + JSON.stringify(res));

						},
						fail: function(err) {
							console.log("fail:" + JSON.stringify(err));
						},
            complete: res => {
              this.$refs.sharePop.close()
            }
					});
				}
			},
			share_gengduo() {
        
				if (this.share_type == 0) {
          let summary = this.share_title + '\n' + this.share_des + '\n\n' + this.shareUrl
					plus.share.sendWithSystem({
            type: 'text',
						content: summary,
            href: this.shareUrl
					});
				} else {
					uni.shareWithSystem({
						type: 'image',
						imageUrl: this.logo_path
					})
				}
        this.$refs.sharePop.close()
			}
		}
	}
</script>

<style lang="scss">
	.pop_bg {
		border-top-right-radius: 16rpx;
		border-top-left-radius: 16rpx;
		text-align: center;

		.title {
			color: #1A1A1A;
			font-size: 32rpx;
		}

		.content-share {
			margin-top: 40rpx;
			display: flex;

			.share_01 {
				display: flex;
				flex-direction: column;
				align-items: center;
				flex: 1;

				image {
					width: 76rpx;
					height: 76rpx;
				}

				text {
					color: #5A5A5A;
					font-size: 24rpx;
				}
			}
		}

		.close_pop {
			color: #FF5A48;
			margin-top: 22rpx;
			height: 88rpx;
			border-top: 1px solid #EFEFEF;
			line-height: 88rpx;
			text-align: center;
			width: 100%;
			font-size: 28rpx;
		}
	}
</style>
