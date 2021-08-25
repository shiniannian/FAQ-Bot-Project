<template>
	<view class="main" @tap="d">
		<span>{{title}}</span>
		<canvas id="id1" canvas-id="firstCanvas" @tap="a"></canvas>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: '欢迎来到双人井字棋小游戏',
				context:"",
				colorx:"#DC143C",
				position:[
					[0,0,0],
					[0,0,0],
					[0,0,0]
				],
				x1:"0",
				y1:"0",
				isclose:"0"
			}
		},
		
		methods: {
	       onReady(){
			   this.context=uni.createCanvasContext('firstCanvas')
			   this.context.setFillStyle(this.colorx)
		   },
		   
		   a(event){
			   // var x=event.touches[0].pageX
			   // var y=event.touches[0].pageY
			   
			   if(this.isclose=="1"){
				   this.title="游戏已结束，点我再来一局"
				   return
			   }
			   
			   this.b(event)
			   
			   // var x=this.x1*80+61
			   // var y=this.y1*80+210			   
			   // console.log(x+":"+y)
			   
			   for(var i=0;i<3;i++){
				   for(var j=0;j<3;j++){
					   if(this.position[i][j]!=0){
						   this.context.beginPath()
						   this.context.arc(i*80+61-30+40,j*80+210-100+40,40,0,2*Math.PI,false)
						   if(this.position[i][j]==1){
						   	   this.context.setFillStyle("#DC143C")
						   }
						   else{
						   	   this.context.setFillStyle("#4B0082")
						   }					   
						   this.context.fill()
					   }					   
				   }
			   }
			   
			   // this.context.beginPath()
			   // this.context.arc(x-30+40,y-100+40,40,0,2*Math.PI,false)
			   // this.context.setFillStyle(this.colorx)
			   // this.context.fill()
			   this.context.draw()
			   
			   this.c()
			   								  
			},
		   b:function(event){
			   var x=event.touches[0].pageX
			   var y=event.touches[0].pageY
			   
			   this.x1=parseInt((x-61)/80)
			   this.y1=parseInt((y-210)/80)
			   
			   if(this.position[this.x1][this.y1]==0){
				   if(this.colorx=="#DC143C"){
					   this.position[this.x1][this.y1]=1
				   }else{
					   this.position[this.x1][this.y1]=2
				   }
				   
				   if(this.colorx=="#DC143C"){
					   this.colorx="#4B0082"
				   }else{
					   this.colorx="#DC143C"
				   }
			   }
		   },
		   
		   c(){
			   //竖一
			   if(this.position[0][0]== this.position[0][1]&&this.position[0][1]==this.position[0][2]){
				   this.e(this.position[0][0])
			   }
			   //竖二
			   if(this.position[1][0]== this.position[1][1]&&this.position[1][1]==this.position[1][2]){
			   				   this.e(this.position[1][0])
			   }
			   //竖三
			   if(this.position[2][0]== this.position[2][1]&&this.position[2][1]==this.position[2][2]){
			   				   this.e(this.position[2][0])
			   }
			   
			   //横一
			   if(this.position[0][0]== this.position[1][0]&&this.position[1][0]==this.position[2][0]){
			   				   this.e(this.position[0][0])
			   }
			   //横二
			   if(this.position[0][1]== this.position[1][1]&&this.position[1][1]==this.position[2][1]){
			   				   this.e(this.position[0][1])
			   }
			   //横三
			   if(this.position[0][2]== this.position[1][2]&&this.position[1][2]==this.position[2][2]){
			   				   this.e(this.position[0][2])
			   }
			   
			   //斜一
			   if(this.position[0][0]== this.position[1][1]&&this.position[1][1]==this.position[2][2]){
			   				   this.e(this.position[0][0])
			   }
			   //斜二
			   if(this.position[2][0]== this.position[1][1]&&this.position[1][1]==this.position[0][2]){
			   				   this.e(this.position[2][0])
			   }
			   
			   var sum=0
			   for(var i=0;i<3;i++){
				   for(var j=0;j<3;j++){
					   if(this.position[i][j]!=0){
						   sum+=1
					   }
				   }
			   }
			   
			   if(sum==9&&this.isclose==0){
				   this.title="和棋，点击我再来一局"
			   }
		   },
		   e(a){
			   if(a!=0){
				   this.isclose=1
				   if(a==1){
					   this.title="红方获胜，点击我再来一局"
					   alert("红方获胜")
				   }else{
					   this.title="蓝方获胜，点击我再来一局"
					   alert("蓝方获胜")
				   }
			   }
		},
		
		d(event){
			var x=event.touches[0].pageX
			var y=event.touches[0].pageY
			if(x>=0&&x<=210&&y>=0&&y<=20){
				for(var i=0;i<3;i++){
					for(var j=0;j<3;j++){
						this.position[i][j]=0
					}
				}
				this.isclose="0"
				this.title="欢迎来到双人井字棋小游戏"
				
				this.context.beginPath()
				this.context.draw()
			}
		  }
		}
		
	}
</script>

<style>
	.main{
		background-color: #C0C0C0;
	}
	
	#id1{
		background-image: url(../../../static/icon/jingziqi.png);
		width: 300px;
		height: 450px;
		margin: 30px;
	}
</style>
