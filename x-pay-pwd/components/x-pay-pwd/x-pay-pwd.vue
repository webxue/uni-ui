<template>
	<view class="content" :class="{show:open}">
		<view class="mask" @click="handleMaskClick"></view>
		
		<view class="wrap native" v-if="type === 0" :style="{top:top,bottom:bottom}">
			<view class="head" v-if="showHead">{{headText}}<text class="close" v-if="showClose" @click="_close">x</text></view>
			<view ref="pwdTxt" class="input" @click="_focusIpt">
				<input ref="pwdIpt" class="hide_ipt" type="tel" maxlength="6" v-model="passwordStr" focus @input="_input"/>
				<view class="pwd_i" v-for="(item,index) in password" :key="index"><text class="pwd" v-if="item"></text></view>
			</view>
			<slot name="center"/>
		</view>
		
		<view class="wrap custom" v-if="type === 1" :style="{top:top,bottom:bottom}">
			<view class="head" v-if="showHead">{{headText}}<text class="close" v-if="showClose" @click="_close">x</text></view>
			<view class="input">
				<input class="pwd_i" type="password" maxlength="1" v-model="pwdArr[0]" disabled />
				<input class="pwd_i" type="password" maxlength="1" v-model="pwdArr[1]" disabled />
				<input class="pwd_i" type="password" maxlength="1" v-model="pwdArr[2]" disabled />
				<input class="pwd_i" type="password" maxlength="1" v-model="pwdArr[3]" disabled />
				<input class="pwd_i" type="password" maxlength="1" v-model="pwdArr[4]" disabled />
				<input class="pwd_i" type="password" maxlength="1" v-model="pwdArr[5]" disabled />
			</view>
			<slot name="center"/>
			<view class="key">
				<view class="key_i" v-for="(key,index) in keys" :key="index" :class="{nobg:key == '' || key == 'del',del:key == 'del'}" @click="inputKey(key)">
					<text v-if="key != 'del'">{{key}}</text>
					<text v-else class="text">x</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		props:{
			maskClick:{//是否允许点击蒙版
				type:Boolean,
				default:true
			},
			top:{//absoute的top值
				type:String,
				default:'20vh'
			},
			bottom:{//absoulute的bottom值
				type:String,
				default:'0rpx'
			},
			showClose:{//是否显示关闭按钮
				type:Boolean,
				default:true
			},
			type:{//密码支付类型 0原生输入框  1自定义输入框
				type:Number,
				default:1
			},
			showHead:{//是否显示头部信息
				type:Boolean,
				default:true
			},
			headText:{//头部信息文字
				type:String,
				default:'请输入支付密码'
			}
		},
		data(){
			return{
				passwordStr:'',//原生需要的字符串密码
				password:['','','','','',''],//原生键盘输入的密码
				open:false,//是否展示
				pwdArr:[],//自定义支付输入的密码
				keys:['1','2','3','4','5','6','7','8','9','','0','del'],//键盘
			}
		},
		methods:{
			_input(){// 监听输入
				const pwdArr = this.passwordStr.split('');
				for(let i = 0;i<6;i++){
					this.password[i] = pwdArr[i];
				}
				if(this.password.length == 6){
					this.$emit('change',{password:this.password.join('')})
				}
			},
			_focusIpt(){// 监听点击按钮使输入框获得焦点
				this.$refs.pwdIpt._focus();
			},
			_open(){// 打开弹窗
				this.open = true;
			},
			_close(){// 关闭弹窗
				this.open = false;
			},
			_clearKey(){// 清空输入
				this.passwordStr = '';
				this.pwdArr = [];
				for(let i = 0;i<6;i++){
					this.password[i] = '';
				}
			},
			handleMaskClick(){//点击蒙版
				if(!this.maskClick) return;
				this._close();
			},
			inputKey(k){// 监听自定义输入
				if(k == '') return;
				if(k != 'del'){
					if(this.pwdArr.length == 6) return;
					this.pwdArr.push(k);
				}else{
					if(this.pwdArr.length == 0) return;
					this.pwdArr.splice(this.pwdArr.length-1,1)
				}
				this.$emit('change',{password:this.pwdArr.join('')})
			},
		}
	}
</script>

<style lang="scss" scoped>
	.content{position: fixed;top: 0rpx;right: 0rpx;bottom: 0rpx;left: 0rpx; justify-content: center;display: flex;transition:.3s;transform: scale3d(0, 0, 0);
		&.show{transform: scale3d(1,1,1);}
		.mask{position: absolute;top: 0;right: 0;bottom: 0;left: 0;background-color: rgba($color: #000000, $alpha: 0.6);z-index:1;}
		.wrap{background-color: #fff;border-radius: 16rpx;padding: 40rpx;height: max-content;z-index: 2;position: absolute;width: 70%;
			.head{text-align: center;font-size: 36rpx;color: #2B2B2B;font-weight: 500;margin-bottom: 36rpx;position: relative;
				.close{position: absolute;right: 0rpx;top: 0rpx;width: 40rpx;height: 40rpx;font-size: 32rpx;color: #646464;display: inline-block;}
			}
			.input{display: flex;margin: 0rpx 0rpx 16rpx;border: 2rpx solid #F1F1F1;border-radius: 16rpx;justify-content: center;position: relative;
				.pwd_i{width: 88rpx;height: 88rpx;border-right:2rpx solid #F1F1F1;text-align: center;font-size: 50rpx;display: flex;align-items: center;justify-content: center;
					&:last-of-type{border-right:none;}
					.pwd{display: inline-block;width: 18rpx;height: 18rpx;background-color: #000;border-radius: 50%;}
				}
				.hide_ipt{position: absolute;top: 0rpx;right: 0rpx;bottom: 0rpx;left: -100%;height: auto;color: transparent;z-index: -99;}
			}
		}
		.custom{width: 100%;border-radius: 16rpx 16rpx 0rpx 0rpx;padding: 40rpx 0rpx 0rpx;
			.head>.close{right: 20rpx;}
			.input{display: flex;margin: 0rpx 41rpx 16rpx;border: 2rpx solid #F1F1F1;border-radius: 16rpx;justify-content: center;
				.pwd_i{width: 108rpx;height: 108rpx;border-right:2rpx solid #F1F1F1;text-align: center;font-size: 50rpx;
					&:last-of-type{border-right:none;}
				}
			}
			.key{padding: 14rpx 12rpx 0rpx;background-color: #D2D5DB;display: flex;flex-wrap: wrap;
				.key_i{width: 234rpx;height: 92rpx;margin-right: 12rpx;text-align: center;line-height: 92rpx;background-color: #fff;margin-bottom: 14rpx;
					border-radius: 10rpx;box-shadow: 0px 2px 0px 0px rgba(132,134,136,1);font-size: 50rpx;color: #000000;font-weight: 500;
					&:nth-of-type(3n){margin-right: 0rpx;}
					&.nobg{background-color: transparent;box-shadow: none;}
					&.del{display: flex;justify-content: center;align-items: center;
						.text{color: #3F434A;}
					}
					&:active{box-shadow: 4rpx 4rpx 5rpx #444;background-color: rgba($color: #000000, $alpha: 0.2);}
				}
			}
		}
	}
</style>
