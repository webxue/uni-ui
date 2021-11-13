# 使用方法
```
<x-pay-pwd 
	ref="xPayPwd" 
	:type="1" 
	:maskClick="true" 
	top="unset" 
	bottom="0rpx" 
	:showClose="false" 
	@change="change" 
	:showHead="true" 
	headText="请输入支付密码"
>
	<template #center>
		<button @click="clear">插槽</button>
	</template>
</x-pay-pwd>
```
```
export default {
	methods: {
		// 监听输入框内容变化
		change({password}){
			console.log(password)
		},
		// 清空输入框内容,一般用于密码输错手动清空
		clear(){
			this.$refs.xPayPwd._clearKey();
		}
	}
}
```
# 属性
| 字段      | 类型    | 默认           | 描述                                     |
| --------- | ------- | -------------- | ---------------------------------------- |
| type      | Number  | 1              | 0原生键盘 1自定义键盘                    |
| maskClick | Boolean | true           | 是否允许点击蒙版                         |
| top       | String  | 20vh           | 中间内容的top值，为absolute的top值       |
| bottom    | String  | 0rpx           | 中间内容的bottom值，为absolute的bottom值 |
| showClose | Boolean | true           | 是否显示关闭按钮                         |
| showHead  | Boolean | true           | 是否显示标题                             |
| headText  | String  | 请输入支付密码 | 标题文本                                 |
# 事件

| 事件名 | 默认参数   | 描述                             |
| ------ | ---------- | -------------------------------- |
| change | {password} | 监听内容输入，参数返回输入的内容 |

# 组件方法
| 方法名 | 描述                             |
| ------ | -------------------------------- |
| _open | 打开弹窗 |
|_close | 关闭弹窗 |
| _clearnKey | 请空输入内容  |

# 插槽
| 插槽名 | 描述                             |
| ------ | -------------------------------- |
| center | 中间插槽 |

# 注意

```
ios下输入框不会自动获取焦点，需要手动点击输入区域
```

# 参与贡献
+ xueshuai(xueshuai_12@163.com)
+ Email：xueshuai_12@163.com
+ GitHub：[GitHub地址](https://github.com/xue-shuai/uni-ui)
+ QQ交流群：[1063233592](https://qm.qq.com/cgi-bin/qm/qr?k=48lCCsUUYgxZh1eQGvJR9FDzqnwwyghJ&jump_from=webapi)
+ 个人博客：[薛小帅](http://blog.xueshuai.top)
+ 个人公众号：叮当Ding

![叮当Ding](https://img-blog.csdnimg.cn/20210202143040150.png)





