<template>
	<div class="home">
		<myHeader :title='title'></myHeader>
		<div class='header-img'></div>
		<div class='content'>
			<p>
				<i>我的步数</i>
				<router-link @click.native='ToReco' to=''>
					打卡记录
				</router-link>
			</p>
			<div class='number'>
				<p>今日步数</p>
				<h3>{{num}}</h3>
			</div>
			<!-- 打卡 -->
			<div class='pun' @click='hanlder' :disabled="isDisabled" :style='{background:btnBgColor}'>
				{{status}}
			</div>
			<!--  -->
			<p class='tit'>每日完成5000步，即可领取5P币</p>
		</div>

		<div class='Ncount'>
			<i>累积收益</i>
			<span>{{Pcount}}&nbsp;P币</span>
		</div>
	</div>
</template>

<script>
	import {
		Toast
	} from 'mint-ui';
	import myHeader from './../components/Header';
	export default {
		data() {
			return {
				title: '计步领P币',
				num: 6525, //记录步数
				status: '打卡', //状态
				Pcount: 30, //P币
				isDisabled: true, //打卡开关,
				btnBgColor: '' //btn背景色
				
			}
		},
		components: {
			myHeader
		},
		methods: {
			hanlder() {
				if (this.isDisabled == true) {
					this.Pcount += 5;
				}
				if (this.isDisabled == false) {
					return;
				}
				Toast({
					message:'打卡成功',
					className:'Toast'
				});
				this.isDisabled = false;
				this.status = '已打卡';
				this.btnBgColor = '#E3E3E3';
				this.$store.state.isRecord=true;	//打卡纪录
				
			},
			// 
			ToReco() {
				if (this.isDisabled == true)
					this.$router.push("/record");
				else
					this.$router.push({
						path: "/record",
						query: {
							stepCount: this.num
						}
					})
			}
		},
		watch: {
			isDisabled(e) {
				if (e == false) {
					this.btnBgColor = '#E3E3E3';
				}
			}
		},
		mounted() {
			if (this.num < 5000) {
				this.isDisabled = false;
				this.status = '未达标';
			}
			if(this.$store.state.isRecord==true){
				this.isDisabled = false;
				this.status = '已打卡';
				this.Pcount += 5;
			}
		
		},
		created(){

		}
	}
</script>

<style scoped lang='scss'>
	.Toast{
		
	}
	.header-img {
		height: 2.72rem;
		background: url('./../assets/img/banner_头图@3x.png') no-repeat;
		background-size: 100% 100%;
	}
	.content {
		border-radius: .1rem;
		width: 6.9rem;
		height: 5.1rem;
		margin: 0 auto;
		background: #fff;
		position: relative;
		top: -.51rem;
		padding: .3rem;
		box-shadow: 0rem 0.02rem 0.1rem 0rem rgba(153, 153, 153, 0.2);
		p {
			margin: 0;
			font-size: .32rem;
			color: #333;
			font-weight: bold;
			text-align: left;
			height: .48rem;
			line-height: .48rem;
			i {
				font-style: normal;
			}
			a {
				width: 1.36rem;
				height: .45rem;
				color: #56B4FB;
				border: 1px solid #56B4FB;
				font-weight: normal;
				float: right;
				border-radius: .23rem;
				text-align: center;
				font-size: .24rem;
				line-height: .45rem;
			}
		}

		.number {
			width: 2.4rem;
			height: 2.4rem;
			background: url('./../assets/img/bg_步数@3x.png') no-repeat;
			background-size: 100% 100%;
			margin: 0 auto;
			text-align: center;
			margin-top: .3rem;

			&::before {
				content: '';
				display: table;
			}

			p {
				color: #9b9b9b;
				font-weight: normal;
				font-size: .24rem;
				margin-top: .5rem;
				text-align: center;
			}

			h3 {
				margin: 0;
				font-size: .54rem;
				color: #666;
				height: .76rem;
				line-height: .76rem;
				margin-top: .14rem;
			}
		}
		.pun {
			display: block;
			border: 0;
			width: 4.84rem;
			height: .6rem;
			line-height: .6rem;
			background-image: linear-gradient(90deg, #ffbf37 0%, #ff8226 100%);
			text-align: center;
			margin: 0 auto;
			margin-top: .3rem;
			border-radius: .3rem;
			color: #fff;
			font-size: .28rem;
		}

		.tit {
			color: #9b9b9b;
			text-align: center;
			font-size: .18rem;
			margin-top: .2rem;
			height: .25rem;
			line-height: .25rem;
			font-weight: normal;
		}
	}

	.Ncount {
		margin: 0 auto;
		height: 1.05rem;
		line-height: 1.05rem;
		width: 6.9rem;
		text-align: left;
		background: #fff;
		box-shadow: 0rem 0.02rem 0.1rem 0rem rgba(153, 153, 153, 0.2);
		padding: 0 .3rem;
		position: relative;
		display: flex;
		i {
			font-size: .32rem;
			font-weight: bold;
         font-style: normal;
         color:#333;
         font-stretch: normal;
         letter-spacing: 0rem;
         font-family: PingFangSC-Semibold;
		}
		span {
			color: #ff9c00;
			font-size: .32rem;
			font-weight: bold;
			position: absolute;
			right:.3rem;
		}
	}

	.home {
		height: 13.34rem;
		width: 100%;
		background-color: #f1f2f4;
	}
</style>
