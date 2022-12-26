<template>
	<view>
		<!-- 标题栏 -->
		<view>
			<view class="title">{{title}}</view>
			<view class="monitor">
				<img src="static/home/monitor.png" style="width: 24px;" alt="">
				<view class="monitor_text">{{monitor}}</view>
			</view>
			<view class="issue">
				<img src="static/home/issue.png" style="width: 24px;" alt="">
				<view class="issue_text">{{issue}}</view>
			</view>
		</view>
		<!-- 筛选内容 -->
		<view class="center">
			<img src="static/home/add.png" style="width: 36rpx;
			margin-left:10px;margin-top:4px" alt="">
			<view style="margin-top: -10px;font-size: 12px;
			margin-left: 8px;color:#A9AAB0">{{title}}</view>
			<view style="width: 320px;height: 25px;background:aliceblue;margin-left: 40px;
			margin-top: -35px;border-radius: 10px;">
			<input type="text" placeholder="请输入标题" style="width: 240px;
			margin-top: 2px;position:absolute;margin-left: 13px;background-color: aliceblue;
			font-size: 15px;">
			<img src="../../static/home/search.png" style="width: 36rpx;float: right;margin-right: 10px;
			margin-top: 4px;"></image>
			</view>
			<view style="float: right;margin-top: -30px;margin-right:10px">
				<img src="static/home/filter.png" style="width: 20px;" alt="">
				<view style="font-size: 10px;color:#A9AAB0;margin-top: -10px;">{{issue}}</view>
			</view>
		</view>
		<view class="main">
		<view
		    v-for="(item, index) in csListArrl"
		    :key="index"
		    :data-index="index" 
		    class="order-item" 
		    @touchstart="drawStart" 
		    @touchmove="drawMove" 
		    @touchend="drawEnd" 
		    :style="'right:'+item.right+'px'">
		        <view class="content">
					<img :src=item.url style="20px;float: left;margin-top: 20px;
					margin-left:20px" alt="">
				</view>
		        <view class="remove" @click="delData(item)">注 销</view>
		        <view class="edit" @click="editData(item)">编 辑</view>
		    </view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title:"编目",
				monitor:"监控",
				issue:"发布",
				screen:"筛选",
				csListArrl:[{
							name:'小A',
							age:'18',
							right: 0,
							url:"static/home/1.png",
							title:'习近平主席视察数博视',
							date:'2022-03-21  10:00:00',
							person:"张大爷",
							info:"待审核"
						},{
							name:'小A',
							age:'18',
							right: 0,
							url:'static/home/1.png',
							title:'习近平主席视察数博视',
							date:'2022-03-21  10:00:00',
							person:"张大爷",
							info:"待审核"
						},{
							name:'小A',
							age:'18',
							right: 0,
							url:'static/home/1.png',
							title:'习近平主席视察数博视',
							date:'2022-03-21  10:00:00',
							person:"张大爷",
							info:"待审核"
						}],
						//左滑默认宽度
						delBtnWidth: 180
			}
		},
		methods: {
			//开始触摸滑动
				drawStart(e) {
					console.log("开始触发");
					var touch = e.touches[0];
					this.startX = touch.clientX;
				},
				//触摸滑动
				drawMove(e) {
					console.log("滑动");
					for (var index in this.csListArrl) {
						this.$set(this.csListArrl[index],'right',0);
					}
					var touch = e.touches[0];
					var item = this.csListArrl[e.currentTarget.dataset.index];
					var disX = this.startX - touch.clientX;
					if (disX >= 20) {
					        if (disX > this.delBtnWidth) {
						    disX = this.delBtnWidth;
					        }
					        this.$set(this.csListArrl[e.currentTarget.dataset.index],'right',disX);
					} else {
						this.$set(this.csListArrl[e.currentTarget.dataset.index],'right',0);
					}
				},
				//触摸滑动结束
				drawEnd(e) {
					console.log("滑动结束");
					var item = this.csListArrl[e.currentTarget.dataset.index];
					if (item.right >= this.delBtnWidth / 2) {
						this.$set(this.csListArrl[e.currentTarget.dataset.index],'right',this.delBtnWidth);
					} else {
						this.$set(this.csListArrl[e.currentTarget.dataset.index],'right',0);
					}
				},
				//删除方法
				delData(item){
					console.log("删除")
					uni.showModal({
					    title: '提示',
					    content: "确认注销该人员？",
					    success: function (res) {
						if (res.confirm) {
							console.log('用户点击确定');
					
						} else if (res.cancel) {
							console.log('用户点击取消');
						}
					    }
					});
				},
				editData(item){
					uni.showModal({
						title: '提示',
						content: "确认编辑该项目？",
						success: function (res) {
							if (res.confirm) {
								console.log('用户点击确定');
							} else if (res.cancel) {
								console.log('用户点击取消');
							}
						}
					});
				}
		},
	}
</script>

<style>
.title{
	font-size: 24px;
	margin-top: 20px;
	margin-left: 20px;
}
.monitor{
	float: right;
	margin-right: 60px;
	height: 40px;
	margin-top:-35px;
}
.monitor_text{
	margin-top: -10px;
	font-size: 12px;
}
.issue{
	margin-right:-60px ;
	height: 40px;
	margin-top:-35px;
	float: right;
}
.issue_text{
	margin-top: -10px;
	font-size: 12px;
}
.center{
	background: white;
	width: 100%;
	height: 40px;
	margin-top: 20rpx;
}
.main{
    width: 90%;
    height: auto;
    margin: 10px auto;
    overflow: hidden
}
.order-item {
    width: 100%;
    display: flex;
    position: relative;
    margin: 10px auto;
    align-items:right ;
    flex-direction: row;
}
.content{
    width: 110%;
    height: 100px;
    margin: 0 auto;
    border: 1px solid #C0C0C0;
    line-height: 100px;
    text-align: center;
}

.remove {
    margin-left:-5%;
    width: 80px;
    height: 100%;
    background-color: red;
    color: #FFFFFF;
    position: absolute;
    top: 0;
    right: -80px;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 16px;
}
.edit{
    width: 80px;
    height: 100%;
    background-color: green;
    color: white;
    position: absolute;
    top: 0;
    right: -160px;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 16px;
}
</style>
