<template>
	 <view class="container">
		<uni-list>
			<uni-list-item v-for="(item,index) in result" :key="index" clickable @click="goDetail(item)">
				<image slot='header' style="display: inline-block;width: 150rpx;height: 150rpx;border-radius: 10rpx;margin: 0 5rpx 0 -30rpx;" :src="item.userPic"></image>
				<text slot="footer" style="width: 600rpx;overflow: hidden;line-clamp: 3;display: -webkit-box;-webkit-box-orient: vertical;text-overflow: ellipsis">{{'['+item.duration+']'+item.title}}</text>
			</uni-list-item>
		</uni-list>
		<uni-load-more :status="status"></uni-load-more>
		<button type="primary" size="mini" style="position: fixed;bottom: 10px;right: 10px;border-radius: 100%;" @click="goTop">
			 <uni-icons type="arrow-up" size="25"></uni-icons>
		</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				uname:'fuck',
				id:'dick',
				href: 'https://uniapp.dcloud.io/component/README?id=uniui',
				// 默认数据，避免数据加载延迟带来的报错
				result:[{
					coverUrl: "https://f7.baidu.com/it/u=1435575170,2755419942&fm=222&app=108&f=JPEG@s_2,w_681,h_381,q_100",
					duration: "05:10",
					id: 14232,
					playUrl: "http://vd2.bdstatic.com/mda-nffjajwjt5md8ysr/cae_h264/1655389051683194253/mda-nffjajwjt5md8ysr.mp4",
					title: "唐山又出名了，唐山烧烤店事件有了1个新消息，网友：拍手叫好",
					userName: "豆豆说事a",
					userPic: "https://pic.rmb.bdstatic.com/bjh/user/f694ec6cb2308252c83b1baaff50173f.jpeg?x-bce-process=image/resize,m_lfit,w_200,h_200&autime=50858"
				}],
				page:0,
				status:'more',
			}
		},
		mounted(){
			this.getData()
		},
		// 触底触发事件
		onReachBottom() {
			this.status='loading';
			uni.request({
					// url:'https://api.apiopen.top/getHaoKanVideo',
					url:'https://api.apiopen.top/api/getHaoKanVideo',
					method:'GET',
					data:{page:++this.page},
					success:res=>{
						this.result=[...this.result,...res.data.result.list];
					}
			});
		},
		// 加载事件
		onLoad() {
			uni.startPullDownRefresh()
		},
		// 下拉刷新事件
		onPullDownRefresh() {
			uni.request({
				url: 'https://api.apiopen.top/api/getHaoKanVideo',
				method: 'GET',
				data: {page:++this.page},
				success: res => {
					this.result=res.data.result.list;
					setTimeout(function(){
						uni.stopPullDownRefresh();
					},1000)
				},
				fail: () => {},
				complete: () => {}
			});
		},
		methods: {
			goTop(){
				uni.pageScrollTo({
					scrollTop: 0,
					duration: 300
				});
			},
			getData(){
				uni.request({
					// url:'https://api.apiopen.top/getHaoKanVideo',
					url:'https://api.apiopen.top/api/getHaoKanVideo',
					method:'GET',
					data:{},
					success:res=>{
						console.log(res);
						this.result=res.data.result.list;
					}
				})
			},
			goDetail(item){
				console.log('$$$',item);
				uni.navigateTo({
					url: `../detail/detail?userPic=${item.userPic}&userName=${item.userName}&title=${item.title}&playUrl=${item.playUrl}`,
					success: res => {},
					fail: () => {},
					complete: () => {}
				});
			}
		}
	}
</script>

<style>
	.container {
		padding: 10px;
		font-size: 14px;
		line-height: 24px;
	}
</style>
