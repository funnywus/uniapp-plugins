<template>
	<view class="print">
		<view class="navigation">
			<view class="navigation_back" @tap="backref">
				<uni-icons type="left" size="24" color="#000"></uni-icons>
			</view>
			<view class="navigation_title">
				打印交易流水
			</view>
			<view class="navigation_record" @tap="toRecord()">
				申请记录
			</view>
		</view>
		<view class="print_con">
			<view class="print_info">
				<view class="print_info_item">
					<view class="print_info_label">
						姓名
					</view>
					<view class="print_info_value">
						{{userInfo.userName.replace(/^.{1}/, '*')}}
					</view>
				</view>
				<view class="print_info_item">
					<view class="print_info_label">
						账户
					</view>
					<view class="print_info_value" @tap="accountFlag = true">
						{{currentCard}}
						<uni-icons type="right" size="16" color="#333" style="margin-left: 10rpx;"></uni-icons>
					</view>
				</view>
				<view class="print_info_item">
					<view class="print_info_label">
						币种
					</view>
					<view class="print_info_value">
						人民币
						<uni-icons type="right" size="16" color="#333" style="margin-left: 10rpx;"></uni-icons>
					</view>
				</view>
			</view>

			<view class="print_types">
				<view class="print_types_title">
					交易类型
				</view>
				<view class="print_types_list">
					<view class="print_types_item" v-for="(item,index) in typeList" :key="index"
						:class="item.value == activeType?'active':''" @tap="changeType(item)">
						{{ item.name }}
					</view>
				</view>
				<view class="print_types_more">
					<view class="print_types_more_label">
						更多筛选
					</view>
					<view class="print_types_more_icon">
						<uni-icons type="bottom" size="18" color="#333"></uni-icons>
					</view>
				</view>
			</view>

			<view class="print_display">
				<view class="print_display_hd">
					<view class="print_display_title">
						交易信息展示
					</view>
					<view class="print_display_preview">
						样例预览
					</view>
				</view>
				<checkbox-group class="uni-flex uni-row checkbox-group"  style="flex-wrap: wrap">
					
					<view class="print_display_list">
						<view class="print_display_item">
							<checkbox checked="true" value="cb3" style="transform: scale(0.7);" class="checkbox">
							 
							</checkbox>
							<view class="print_display_item_label">
								完整展示对方账号
							</view>
						</view>
						<view class="print_display_item">
							<checkbox checked="true" value="cb3" style="transform: scale(0.7);" class="checkbox">
								 
							</checkbox>
							<view class="print_display_item_label">
															完整展示对方户名
							</view>
						</view>
						<view class="print_display_item">
							<checkbox checked="true" value="cb3" style="transform: scale(0.7);" class="checkbox">
								 
							</checkbox>
							<view class="print_display_item_label">
																展示交易地点/附言
							</view>
						</view>
					</view>
				  </checkbox-group>
				
			</view>

			<view class="print_date">
				<view class="print_date_hd">
					<view class="print_date_title">
						查询范围
					</view>
				</view>
				<view class="print_date_item">
					<view class="print_date_label">
						起始日期
					</view>
					<view class="print_date_value">
							<view  @tap="dateVisible1=true">{{startDate ? startDate : '请选择起始日期'}}</view>
						<uni-icons type="right" size="16" color="#333" style="margin-left: 10rpx;"></uni-icons>
					</view>
				</view>
				<view class="print_date_item">
					<view class="print_date_label">
						终止日期
					</view>
					<view class="print_date_value">
					<view  @tap="dateVisible2=true">{{endDate ? endDate : '请选择起始日期'}}</view>
						<uni-icons type="right" size="16" color="#333" style="margin-left: 10rpx;"></uni-icons>
					</view>
				</view>
				<view class="print_date_btns">
					<view class="print_date_btn" :class="{ active: currentDate === 0 }" @click="handleSelectDate(0)">
						近三月
					</view>
					<view class="print_date_btn" :class="{ active: currentDate === 1 }" @click="handleSelectDate(1)">
						近一年
					</view>
					<view class="print_date_btn" :class="{ active: currentDate === 2 }" @click="handleSelectDate(2)">
						近三年
					</view>
				</view>
			</view>

			<view class="print_way">
				<view class="print_way_item">
					<view class="print_way_label">
						发送方式
					</view>
					<view class="print_way_value" @tap="isShow = !isShow">
						邮箱发送
						<uni-icons type="right" size="16" color="#333" style="margin-left: 10rpx;"></uni-icons>
					</view>
				</view>
				
				<view class="print_way_item">
					<view class="print_way_label" style="width: 120rpx;">
						发送邮箱
					</view>
					<view class="print_way_value">
						<input style="text-align: right;" placeholder="" v-model="mails" />
					</view>
				</view>
				
				<view v-show="isShow">
					<view class="print_way_item">
						<view class="print_way_label" style="width: 120rpx;">
							流水日期
						</view>
						<view class="print_way_value">
							<input style="text-align: right;" placeholder="" v-model="date" />
						</view>
					</view>
					
					<view class="print_way_item">
						<view class="print_way_label" style="width: 120rpx;">
							流水编号
						</view>
						<view class="print_way_value">
							<input style="text-align: right;" placeholder="" v-model="code" />
						</view>
					</view>
				</view>
				
				<view class="print_way_btn">
					<view class="print_way_btn_inner" @tap="submit">
						提交
					</view>
				</view>

				<view class="print_way_tip">
					1.收费标准:手机银行渠道打印交易流水暂免服务费。<br /><br />
					2.由于文件传输大小限制，若您的单次要求打印的交易笔数超过1万笔，可能存在明细显示不全的情况，建议您分多次进行打印。<br /><br />
					3.本功能仅支持打印2012年1月1日之后的交易流水，若想要打印更早的交易明细，您可以前往我行网点柜面申请打印。感谢您的理解和支持。
				</view>
			</view>
		</view>
		
				<!-- <view class="item" @tap="dateVisible1=true">日期1</view> -->
		
		<!-- {{result}} -->
		<w-picker
			:visible.sync="dateVisible1"
			mode="date" 
			startYear="2017" 
			endYear="2029"
			:value="startDate"
			:current="false"
			fields="day"
			@confirm="onConfirm1($event,'date1')"
			@cancel="onCancel"
			:disabled-after="false"
			ref="date1"
		></w-picker>
		
		<w-picker
			:visible.sync="dateVisible2"
			mode="date" 
			startYear="2017" 
			endYear="2029"
			:value="endDate"
			:current="false"
			fields="day"
			@confirm="onConfirm2($event,'date1')"
			@cancel="onCancel"
			:disabled-after="false"
			ref="date2"
		></w-picker>



		<view class="print_password" v-if="passwordFlag == true">
			<view class="print_password_con">
				<view class="print_password_hd">
					<view class="print_password_title">
						请输入密码
					</view>
					<view class="print_password_close" @tap="closePwd">
						<uni-icons type="closeempty" size="20" color="#333"></uni-icons>
					</view>
				</view>
				<view class="print_password_title2">
					请输入 <text>借记卡(1225)</text>6位交易密码
				</view>
				<view class="print_password_input">
					<view class="print_password_li">
						<text v-if="password.length >= 1">*</text>
					</view>
					<view class="print_password_li">
						<text v-if="password.length >= 2">*</text>
					</view>
					<view class="print_password_li">
						<text v-if="password.length >= 3">*</text>
					</view>
					<view class="print_password_li">
						<text v-if="password.length >= 4">*</text>
					</view>
					<view class="print_password_li">
						<text v-if="password.length >= 5">*</text>
					</view>
					<view class="print_password_li">
						<text v-if="password.length >= 6">*</text>
					</view>
					<input type="text" maxlength="6" v-model="password">
				</view>
				<view class="print_password_btn">
					<view class="print_password_btn_inner" :class="password.length == 6?'active':''" @tap="surePwd">
						确认
					</view>
				</view>
			</view>
		</view>

		<view class="mingxi_account" v-if="accountFlag == true">
			<view class="mingxi_account_con">
				<view class="mingxi_account_hd">
					<view class="mingxi_account_title">
						选择账户
					</view>
					<view class="mingxi_account_close" @tap="accountFlag = false">
						<uni-icons type="closeempty" size="18" color="#000"></uni-icons>
					</view>
				</view>
				<view class="mingxi_account_list">
					<view class="mingxi_account_item" v-for="(item,index) in cardList" :key="index"
						:class="cardId == item.id?'active':''" @tap="changeAccount(item)">
						<view class="mingxi_account_item_icon">
							<image src="@/static/mingxi/account.jpg" mode="widthFix"></image>
						</view>
						<view class="mingxi_account_item_name">
							{{ item.name }}
						</view>
						<view class="mingxi_account_item_right">
							<uni-icons type="checkmarkempty" size="18" color="#666"></uni-icons>
						</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import * as api from "../../common/api.js"
	import * as common from "../../common/common.js"
	export default {
		data() {
			return {
				dateVisible1:false,
				dateVisible2:false,
				result1: '',
				result2: '',
				currentDate: 0,
				activeType: 1,
				date: "",
				code: "",
				isShow: false,

				currentCard: '所有借记账户',
				typeList: [{
						name: '全部',
						value: 1
					},
					{
						name: '收入',
						value: 2
					},
					{
						name: '支出',
						value: 3
					},
					{
						name: '网上支付',
						value: 4
					},
					{
						name: '转账汇款',
						value: 5
					},
					{
						name: '信用卡还款',
						value: 6
					},
					{
						name: '工资奖金',
						value: 7
					},
				],


				password: '',
				passwordFlag: false,

				accountFlag: false,
				cardId: '',
				cardList: [],
				startDate: '2024-11-30',
				endDate: '2024-11-30',
				userInfo: {},
				mails: null
			};
		},
		onLoad() {

			this.userInfo = uni.getStorageSync("userinfo")
			this.getcardList()
		},
		methods: {
			onConfirm1(res,type){
				this.startDate=res.result;
				console.log(res)
			},
			onConfirm2(res,type){
				this.endDate=res.result;
				console.log(res)
			},
			handleSelectDate (index) {
				console.log(12312)
				this.currentDate = index
			},
			backref() {
				uni.navigateBack({
					delta: 1
				})
			},
			getcardList() {
				this.cardList = [
					{
					id: 0,
					name: '所有借记账户'
				},
				]
				api.cardList().then(res => {
					let arr = res.list.map(obj => {
						return {
							"id": obj["id"],
							"name": obj["type"] + "(" + common.cardNumber2(obj["cardNumber"]) + ")"
						};
					});

					arr.forEach(element => this.cardList.push(element));
				})
			},
			submit() {
				this.passwordFlag = true;
			},
			closePwd() {
				this.password = '';
				this.passwordFlag = false;
			},
			surePwd() {
				this.password = '';
				this.passwordFlag = false;
				this.export()
			},
			export() {
				api.exportsFlow({
					cardId: this.cardId,
					startDate: this.startDate,
					endDate: this.endDate,
					email: this.mails,
					date: this.date,
					code: this.code,
					userId: this.userInfo.userId,
				}).then(res => {
					uni.navigateTo({
						url: `success`
					})
					}
				)
			},
			changeType(item) {
				this.activeType = item.value;
			},
			changeEndDate(e) {
				this.endDate = e;
			},
			changeStartDate(e) {
				this.startDate = e;
			},
			changeAccount(item) {
				this.cardId = item.id;
				this.currentCard = item.name
				this.accountFlag = false;
			},
			toRecord() {
				uni.navigateTo({
					url: '/pages/print/record'
				})
			}
		}
	}
</script>

<style lang="scss">
	::v-deep .uni-date-x .icon-calendar {
		display: none;
	}

	page {
		background: rgb(242, 249, 254);
	}

	.navigation {
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		display: flex;
		justify-content: center;
		align-items: center;
		padding: 40rpx 32rpx 24rpx;
		background-color: #fff;

		.navigation_back {
			position: absolute;
			left: 32rpx;
		}

		.navigation_title {
			color: #000;
			font-size: 36rpx;
			font-weight: 500;
		}

		.navigation_record {
			position: absolute;
			right: 32rpx;
			color: rgb(17, 26, 269);
			font-size: 28rpx;
		}
	}

	.print_con {
		padding-top: 110rpx;

		.print_info {
			background-color: #fff;

			.print_info_item {
				padding: 32rpx 24rpx;
				display: flex;
				align-items: center;
				justify-content: space-between;

				.print_info_label {
					color: #666;
					font-size: 30rpx;
				}

				.print_info_value {
					color: #333;
					font-size: 30rpx;
				}
			}
		}

		.print_types {
			margin-top: 34rpx;
			padding: 32rpx 24rpx;
			background-color: #fff;

			.print_types_title {
				color: #000;
				font-size: 32rpx;
				font-weight: 500;
			}

			.print_types_list {
				display: flex;
				flex-wrap: wrap;
				gap: 24rpx;
				margin-top: 40rpx;
				margin-bottom: 40rpx;

				.print_types_item {
					width: 31%;
					height: 70rpx;
					border: 1rpx solid rgb(17, 26, 269);
					color: rgb(17, 26, 269);
					border-radius: 6rpx;
					font-size: 30rpx;
					display: flex;
					justify-content: center;
					align-items: center;

					&.active {
						background: linear-gradient(145deg, rgb(17, 26, 269), rgb(72, 127, 239));
						color: #fff;
					}
				}
			}

			.print_types_more {
				display: flex;
				justify-content: space-between;
				align-items: center;

				.print_types_more_label {
					color: rgb(17, 26, 269);
					font-size: 30rpx;
				}
			}
		}

		.print_display {
			margin-top: 32rpx;
			padding: 32rpx 24rpx;
			background-color: #fff;

			.print_display_hd {
				display: flex;
				align-items: center;
				justify-content: space-between;

				.print_display_title {
					color: #000;
					font-size: 32rpx;
					font-weight: 500;
				}

				.print_display_preview {
					color: rgb(72, 127, 239);
					font-size: 28rpx;
				}
			}

			.print_display_list {
				margin-top: 40rpx;
				display: flex;
				justify-content: space-between;
				flex-wrap: wrap;

				.print_display_item {
					display: flex;
					align-items: center;
					width: 50%;
					margin-bottom: 32rpx;
					.checkbox {
						/deep/ .uni-checkbox-input-checked {
							color: #ffffff!important;
							background: #999999!important;
						}
						
					}
					.print_display_item_check {
						width: 32rpx;
						height: 32rpx;
						border: 1rpx solid #ccc;
						border-radius: 6rpx;
					}

					.print_display_item_label {
						color: #999;
						font-size: 26rpx;
						margin-left: 8rpx;
					}
				}
			}
		}

		.print_date {
			margin-top: 32rpx;
			padding: 32rpx 24rpx;
			background-color: #fff;

			.print_date_hd {
				display: flex;
				align-items: center;
				justify-content: space-between;

				.print_date_title {
					color: #000;
					font-size: 32rpx;
					font-weight: 500;
				}
			}

			.print_date_item {
				padding: 30rpx 0;
				border-bottom: 1rpx solid #eee;
				display: flex;
				justify-content: space-between;
				align-items: center;

				.print_date_label {
					color: #333;
					font-size: 28rpx;
				}

				.print_date_value {
					display: flex;
					align-items: center;
					color: #333;
					font-size: 28rpx;
				}
			}

			.print_date_btns {
				padding: 30rpx 0;
				display: flex;
				justify-content: space-between;
				align-items: center;
				
				.print_date_btn {
					width: 31%;
					height: 70rpx;
					border: 1rpx solid rgb(16, 26, 170);
					color: rgb(16, 26, 170);
					font-size: 30rpx;
					display: flex;
					justify-content: center;
					align-items: center;
					&.active {
						color: #ffffff;
						background-color: blue;
						border-color: blue;
					}
				}
			}
		}

		.print_way {
			margin-top: 32rpx;
			padding: 32rpx 24rpx;
			background-color: #fff;

			.print_way_item {
				padding: 30rpx 0;
				border-bottom: 1rpx solid #eee;
				display: flex;
				justify-content: space-between;
				align-items: center;

				.print_way_label {
					color: #333;
					font-size: 28rpx;
				}

				.print_way_value {
					color: #333;
					font-size: 28rpx;
				}
			}

			.print_way_btn {
				padding: 32rpx 50rpx;

				.print_way_btn_inner {
					display: flex;
					justify-content: center;
					align-items: center;
					color: #fff;
					font-size: 30rpx;
					height: 90rpx;
					border-radius: 8rpx;
					background: linear-gradient(145deg, rgb(17, 26, 269), rgb(72, 127, 239));
				}
			}

			.print_way_tip {
				margin-top: 45rpx;
				color: #999;
				font-size: 30rpx;
				line-height: 1.5;
			}
		}
	}

	.print_password {
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-color: rgba(0, 0, 0, .7);
		z-index: 10;

		.print_password_con {
			position: absolute;
			top: 50%;
			left: 50%;
			transform: translate(-50%, -50%);
			z-index: 3;
			border-radius: 10rpx;
			background-color: #fff;
			padding: 40rpx 32rpx;
			width: 95%;

			.print_password_hd {
				display: flex;
				align-items: center;
				justify-content: center;
				position: relative;

				.print_password_title {
					color: #000;
					font-size: 34rpx;
					font-weight: 600;
				}

				.print_password_close {
					position: absolute;
					right: 0;
				}
			}

			.print_password_title2 {
				margin-top: 40rpx;
				text-align: center;
				font-size: 30rpx;
				color: #333;

				text {
					color: rgb(227, 66, 52);
				}
			}

			.print_password_input {
				display: flex;
				align-items: center;
				justify-content: center;
				position: relative;
				margin-top: 24rpx;
				height: 90rpx;

				.print_password_li {
					width: 16%;
					height: 90rpx;
					border: 1rpx solid #eee;
					color: #333;
					font-size: 32rpx;
					display: flex;
					justify-content: center;
					align-items: center;
				}

				input {
					position: absolute;
					top: 0;
					left: 0;
					opacity: 0;
					width: 100%;
					height: 100%;
				}
			}

			.print_password_btn {
				margin-top: 32rpx;
				padding: 0 40rpx;

				.print_password_btn_inner {
					width: 100%;
					height: 100rpx;
					background: linear-gradient(145deg, rgb(17, 26, 269), rgb(72, 127, 239));
					color: #fff;
					font-size: 34rpx;
					display: flex;
					justify-content: center;
					align-items: center;
					border-radius: 8rpx;
					opacity: .6;

					&.active {
						opacity: 1;
					}
				}
			}
		}
	}

	.mingxi_account {
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		z-index: 10;
		background-color: rgba(0, 0, 0, .4);

		.mingxi_account_con {
			position: absolute;
			bottom: 0;
			left: 0;
			width: 100%;
			background-color: #fff;
			padding: 32rpx 24rpx 100rpx;

			.mingxi_account_hd {
				display: flex;
				justify-content: center;
				align-items: center;
				position: relative;

				.mingxi_account_title {
					color: #000;
					font-size: 32rpx;
					font-weight: 500;
				}

				.mingxi_account_close {
					position: absolute;
					right: 0;
				}
			}

			.mingxi_account_list {
				margin-top: 45rpx;

				.mingxi_account_item {
					display: flex;
					padding: 24rpx 0;
					align-items: center;
					border-bottom: 1rpx solid #eee;

					.mingxi_account_item_icon {
						image {
							width: 40rpx;
							height: auto;
						}
					}

					.mingxi_account_item_name {
						font-size: 32rpx;
						color: #333;
						margin-left: 32rpx;
					}

					.mingxi_account_item_right {
						display: none;
						position: absolute;
						right: 24rpx;
					}

					&.active {
						.mingxi_account_item_right {
							display: block;
						}
					}
				}
			}
		}
	}
</style>