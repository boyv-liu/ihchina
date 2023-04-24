<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	/*每个页面公共css */
	@import url('./font.scss');
	view{
		font-size: 32rpx;
		color: #333;
		font-family: 'fzqkbysjw';
	}
	i{
		font-weight: 600;
		color: #fff;
	}

</style>
