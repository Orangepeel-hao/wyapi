<template>
	<view style="display: flex;flex-direction: column;">
		<uni-card :title="userName" :thumbnail="userPic" :border='false' :is-shadow="false">
			<text>{{title}}</text>
		</uni-card>
		<uni-card>
			<video slot='cover' style="width: 100%;" :src="playUrl"></video>
		</uni-card>
	</view>
</template>

<script>
	export default {
		data() {
			return {
					playUrl: "http://vd2.bdstatic.com/mda-nffjajwjt5md8ysr/cae_h264/1655389051683194253/mda-nffjajwjt5md8ysr.mp4",
					title: "唐山又出名了，唐山烧烤店事件有了1个新消息，网友：拍手叫好",
					userName: "豆豆说事a",
					userPic: "https://pic.rmb.bdstatic.com/bjh/user/f694ec6cb2308252c83b1baaff50173f.jpeg?x-bce-process=image/resize,m_lfit,w_200,h_200&autime=50858"
			}
		},
		onLoad(e) {
			console.log(e);
			this.playUrl=e.playUrl;
			this.title=e.title;
			this.userName=e.userName;
			this.userPic=e.userPic;
		},
	}
</script>

<style>

</style>
