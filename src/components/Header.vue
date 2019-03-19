<template>
	<div class='header'>
	 <img src="./../assets/img/back.png" alt="" @click='hist'>
	 <i>{{title}}</i>
	 <div class='header-right'>
		<img src="./../assets/img/more.png" alt="">
		<span></span>
		<img src="./../assets/img/close.png" alt="">
	 </div>
   </div>
</template>

<script>
   export default{
      data(){
         return {
            
         }
      },
      methods:{
         hist(){
            this.$router.go(-1);
         }
      },
      props:['title']
   }
</script>

<style scoped lang='scss'>
.header{
	width:100%;
	background:#2EA2FA;
	height:1rem;
	color:#fff;
	display: flex;
	padding-left:.3rem;
	padding-right:.14rem;
	align-items: center;
	justify-content:space-between;
	position: relative;
	&>img{
		width:.36rem;
		height:.36rem;
	}
	i{
		padding-right:.5rem;
		font-size:.36rem;
		font-style: normal;
	}
	.header-right{
		width:1.74rem;
		height:.64rem;
		position:absolute;
		right:.14rem;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius:.32rem;
		background: rgba(0, 0, 0, 0.3);
		&>span{
			display: inline-block;
			height:.4rem;
			border-right:1px solid #fff;
			margin:0 .25rem;
			background-color: #ffffff;
			opacity: 0.2;
		}
		& img:first-child{
			width:.37rem;
			height:.13rem;
		}
		& img:last-child{
			width: .35rem;
			height:.35rem;
			
		}
	}
}
  
</style>
