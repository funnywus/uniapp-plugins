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
	page {
		background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
		min-height: 100vh;
	}

	/* 按钮渐变样式 */
	.gradient-btn {
		background: linear-gradient(45deg, #4facfe 0%, #00f2fe 100%);
		color: #ffffff;
		border: none;
		border-radius: 8px;
		padding: 12px 24px;
		transition: all 0.3s ease;
	}
	
	.gradient-btn:active {
		transform: scale(0.98);
		opacity: 0.9;
	}

	/* 卡片渐变样式 */
	.gradient-card {
		background: linear-gradient(120deg, #fdfbfb 0%, #ebedee 100%);
		border-radius: 12px;
		box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
		padding: 16px;
		margin: 10px;
	}

	/* 标题渐变文字 */
	.gradient-text {
		background: linear-gradient(to right, #4facfe, #00f2fe);
		-webkit-background-clip: text;
		color: transparent;
		font-weight: bold;
	}

	/* 分割线渐变 */
	.gradient-divider {
		height: 2px;
		background: linear-gradient(to right, rgba(79,172,254,0.2), rgba(0,242,254,0.8), rgba(79,172,254,0.2));
		margin: 10px 0;
	}

	/* 输入框样式 */
	.custom-input {
		border: 1px solid #e0e0e0;
		border-radius: 6px;
		padding: 8px 12px;
		background: rgba(255, 255, 255, 0.9);
		transition: all 0.3s ease;
	}

	.custom-input:focus {
		border-color: #4facfe;
		box-shadow: 0 0 0 2px rgba(79,172,254,0.2);
	}

	/* 列表项悬停效果 */
	.list-item {
		transition: all 0.3s ease;
		border-radius: 6px;
	}

	.list-item:active {
		background: linear-gradient(120deg, #fdfbfb 0%, #ebedee 100%);
		transform: translateX(4px);
	}
</style>
