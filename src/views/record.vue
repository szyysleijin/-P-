<template>
	<div class='record'>
		<header_D :title='title'></header_D>
		<div class='record_date'>
			<!-- 年 -->
			<div class='year'>
				<img src="./../assets/img/ic_left@3x.png" @click='leftYear' alt="">
				<i>{{year}}年{{month}}月</i>
				<img src="./../assets/img/右@3x.png" @click='rightYear' alt="">
			</div>
			<!-- 星期 -->
			<div class='week'>
				<ul>
					<li v-for='(item,i) of weekList' :class='getWeekClass==item?"nowWeek":""'>{{item}}</li>
				</ul>
			</div>
			<!-- 日 -->
			<div class='day'>
				<ul>
					<!-- 空出位子， 显示对应的星期 -->
					<li v-for='(item,i) of nowWeek'></li>
					<!-- 循环每月多少天 -->
					<li v-for='(item,i) of dayCount'>
						<!-- 当天才对应的class nowDay -->
						<!--  -->
						<span :class='i+1==day?"nowDay":""'>{{i+1}}</span>
						<!-- 已打卡 绿色图标 -->
						<i v-for='(_item,_i) of monthList' v-if='i+1== _item.day && _item.month==month && _item.stepCount>5000 && _item.year==year' class='stepOve'></i>
						<!-- 显示打过卡的数据 -->
						<i v-for='(_item,_i) of monthList' v-if='i+1== _item.day && _item.month==month && _item.stepCount>5000 && _item.year==year'>{{_item.stepCount}}步</i>
					</li>
				</ul>
			</div>
		</div>
	</div>
</template>

<script>
	import header_D from './../components/Header';
	export default {
		data() {
			return {
				year: '', //年
				month: '', //月
				day: '', //日
				week: '', //星期
				dayCount: '', //当前月有几天
				nowWeek: '', //当前月1号星期几
				title: '打卡记录',
				weekList: ['日', '一', '二', '三', '四', '五', '六'], //星期
				stepCount: '', //打卡记录步数 
				monthList: [ //测试记步数据
					// {month:3,day:15,stepCount:this.stepCount},     
					{
						year:2019,
						month: 3,
						day: 2,
						stepCount: '6525'
					},
					{
						year:2019,
						month: 3,
						day: 11,
						stepCount: '5252'
					}, //测试记步数据
					{
						year:2019,
						month: 5,
						day: 1,
						stepCount: '43211'
					}, //测试记步数据
					{
						year:2019,
						month: 5,
						day: 5,
						stepCount: '9876'
					}, //测试记步数据
					{
						year:2019,
						month: 5,
						day: 27,
						stepCount: '5555'
					}, //测试记步数据
					{
						year:2019,
						month: 4,
						day: 1,
						stepCount: '8888'
					}, //测试记步数据
					{
						year:2019,
						month: 4,
						day: 13,
						stepCount: '5555'
					}, //测试记步数据
					{
						year:2019,
						month: 4,
						day: 28,
						stepCount: '6666'
					}, //测试记步数据
					{
						year:2019,
						month: 2,
						day: 3,
						stepCount: '8888'
					}, //测试记步数据
					{
						year:2019,
						month: 1,
						day: 5,
						stepCount: '5555'
					}, //测试记步数据
					{
						year:2019,
						month: 2,
						day: 18,
						stepCount: '6666'
					}, //测试记步数据
					{
						year:2019,
						month: 1,
						day: 15,
						stepCount: '5555'
					}, //测试记步数据
					{
						year:2019,
						month: 2,
						day: 28,
						stepCount: '4322'
					}, //测试记步数据
					{
						year:2019,
						month: 1,
						day: 28,
						stepCount: '4322'
					}, //测试记步数据
					{
						year:2019,
						month: 6,
						day: 2,
						stepCount: '5678'
					}, //测试记步数据
					{
						year:2019,
						month: 6,
						day: 15,
						stepCount: '7890'
					}, //测试记步数据
					{
						year:2019,
						month: 6,
						day: 28,
						stepCount: '9876'
					}, //测试记步数据
				],
			}
		},
		wathch: {

		},
		computed: {
			getWeekClass() {
				if (this.week == 1) return '一';
				if (this.week == 2) return '二';
				if (this.week == 3) return '三';
				if (this.week == 4) return '四';
				if (this.week == 5) return '五';
				if (this.week == 6) return '六';
				if (this.week == 0) return '日';
			}
		},
		methods: {
			// 上个月
			leftYear() {
				this.month -= 1;
				if (this.month == 0) {
					this.year -= 1;
					this.month = 12;
				}
				this.monthCount();
			},
			// 下个月
			rightYear() {
				this.month += 1;
				if (this.month == 13) {
					this.year += 1;
					this.month = 1;
				}
            this.monthCount();
			},
         //上下月计算
         monthCount(){
            this.dayCount = this.getdayCount(this.year, this.month, 0); //获取当前月总天数
            let str = `${this.year},${this.month},01`;
            let myDate = new Date(str);
            this.nowWeek = myDate.getDay();
            this.week = myDate.getDay();
            let str1 = `${this.year},${this.month},${this.day}`;
            let myDate1 = new Date(str1);
            this.week = myDate1.getDay();
         },
			//计算当前月有几天
			getdayCount(year, month, n) {
				let curDate = new Date(year, month, 0);
				// this.pushObj()
				return curDate.getDate();
			},
			//获取当前月1号星期几
			getNowWeek(year_, month_) {
				let year = new Date().getFullYear(); //年
				let month = new Date().getMonth() + 1; //月
				let str = `${year},${month},01`;
				let myDate = new Date(str);
				return myDate.getDay(); //获取当前1月星期几(0-6,0代表星期天)
			}
		},
		mounted() {
			this.dayCount = this.getdayCount(this.year, this.month, 0); //获取当前月总天数
			this.nowWeek = this.getNowWeek();//获取当前1月星期几(0-6,0代表星期天)
			this.year = new Date().getFullYear(); //年
			this.month = new Date().getMonth() + 1; //月
			this.day = new Date().getDate(); //日
			this.week = new Date().getDay(); //周几
			this.stepCount = this.$route.query.stepCount; //当天打卡，传过来的步数
			if (this.stepCount) //如果打卡
				this.monthList.push({
               year:this.year,
					month: this.month,
					day: this.day,
					stepCount: this.stepCount
				}); //15号今天的数据
		},
		components: {
			header_D
		}
	}
</script>

<style lang='scss' scoped>
	li {
		list-style: none;
	}

	.stepOve {
		background: #EAF6FF;
		border-radius: .39rem;
		width: .48rem;
		height: .48rem;
		position: absolute;
		color: #666;
	}

	.nowWeek {
		color: #2ea2fa !important;
	}

	.nowDay {
		background: #2EA2FA;
		color: #fff !important;
		border-radius: .39rem;
		width:.6rem !important;
		height:.6rem !important;
		line-height: .6rem !important;
		margin-top:-.08rem;
	}

	.record_date {
		margin-top: .2rem;
		background: #fff;
	}

	.day {
		background-color: #fcfcfc;
		padding-top:.2rem;
		ul li,
			{
			float: left;
			width: 14%;
			height: 1rem;
			display: flex;
			flex-direction: row;
			flex-wrap: wrap;
			justify-content: center;

			span {
				font-size: .22rem;
				color: #666;
				text-align: center;
				display: inline-block;
				width: .48rem;
				height: .48rem;
				line-height: .48rem;
				z-index: 2;
			}

			i {
				display: inline-block;
				color: #2ea2fa;
				font-size: .24rem;
				font-style: normal;
			}
		}
	}

	.week {
		background-color: #fcfcfc;

		ul li {
			float: left;
			width: 14%;
			height: .6rem;
			line-height: .6rem;
			font-size: .22rem;
			color: #cbc9d5;
		}
	}

	.year {
		height: 1.05rem;
		line-height: 1.05rem;
		color: #333;
		font-size: .32rem;
		display: flex;
		justify-content: center;
		align-items: center;

		i {
			display: inline-block;
			padding: 0 .5rem;
			font-style: normal;
		}

		img {
			width: .22rem;
			height: .4rem;
		}
	}

	.record {
		background: #F1F2F4;
		height: 13.34rem;
	}

	ul,
	li {
		padding: 0;
		margin: 0;
	}
</style>
