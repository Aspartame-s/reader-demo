<template>
<div class="ebook">
	<div class="title-wrapper">
		<div class="left">
			<span class="icon-back icon"></span>
		</div>
		<div class="right">
			<div class="icon-wrapper">
				<span class="icon-cart icon"></span>
			</div>
			<div class="icon-wrapper">
				<span class="icon-person icon"></span>
			</div>
			<div class="icon-wrapper">
				<span class="icon-more icon"></span>
			</div>
		</div>
	</div>
	<div class="read-wrapper">
		<div id="read"></div>
		<div class="mask">
			<div class="left" @click="prevPage"></div>
			<div class="center"></div>
			<div class="right" @click="nextPage"></div>
		</div>
	</div>
	<div class="menu-wrapper">
		<div class="icon-wrapper">
			<span class="icon-menu icon"></span>
		</div>
		<div class="icon-wrapper">
			<span class="icon-progress icon"></span>
		</div>
		<div class="icon-wrapper">
			<span class="icon-bright icon"></span>
		</div>
		<div class="icon-wrapper">
			<span class="icon-a icon">A</span>
		</div>
	</div>
</div>
</template>

<script>
import Epub from 'epubjs'
const DOWNLOAD_URL = '/static/2018_Book_AgileProcessesInSoftwareEngine.epub'
export default {
	data() {
		return {
		};
	},
	methods: {
		//电子书的解析和渲染
		showEpub() {
			//生成book对象
			this.book = new Epub(DOWNLOAD_URL)
			//生成rendition，通过book.renderTo方法实现
			this.rendition = this.book.renderTo('read', {
				width: window.innerWidth,
				height: window.innerHeight
			})
			//通过rendition.display方法渲染电子书
			this.rendition.display()
		},
		prevPage() {
			if(this.rendition) {
				this.rendition.prev()
			}
		},
		nextPage() {
			if(this.rendition) {
				this.rendition.next()
			}
		}
	},
	created() {},
	mounted() {
		this.showEpub()
	}
};
</script>
<style lang="scss" scoped>
	@import 'assets/styles/global';
	.ebook {
		position: relative;
		.title-wrapper {
			position: absolute;
			top: 0;
			left: 0;
			width: 100%;
			height: px2rem(48);
			background-color: #fff;
			z-index: 101;
			display: flex;
			box-shadow: 0 px2rem(8) px2rem(8) rgba(0,0,0,0.15);
			.left {
				flex: 0 0 px2rem(60);
				@include center
			}
			.right {
				flex: 1;
				display: flex;
				justify-content: flex-end;
				.icon-wrapper {
					flex: 0 0 px2rem(40);
					@include center;
					.icon-cart {
						font-size:px2rem(22);
					}
				}
			}
		}
		.read-wrapper {
			.mask {
				position: absolute;
				top: 0;
				left: 0;
				width: 100%;
				height: 100%;
				z-index: 100;
				display: flex;
				.left {
					flex: 0 0 px2rem(100);
				}
				.center {
					flex: 1;
				}
				.right {
					flex: 0 0 px2rem(100);
				}
			}
		}
		.menu-wrapper {
			position: absolute;
			bottom: 0;
			left: 0;
			width: 100%;
			height: px2rem(48);
			background-color: #fff;
			z-index: 101;
			display: flex;
			box-shadow: 0 px2rem(-8) px2rem(8) rgba(0,0,0,0.15);
			.icon-wrapper {
				flex: 1;
				@include center;
				.icon-progress {
					font-size: px2rem(28);
				}
				.icon-bright {
					font-size: px2rem(24);
				}
			}
		}
	}
</style>