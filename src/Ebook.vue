<template>
<div class="ebook">
	<title-bar :titleMenu="titleMenu"></title-bar>
	<div class="read-wrapper">
		<div id="read"></div>
		<div class="mask">
			<div class="left" @click="prevPage"></div>
			<div class="center" @click="toggleTitleMenu"></div>
			<div class="right" @click="nextPage"></div>
		</div>
	</div>
	<menu-bar :titleMenu="titleMenu" :fontList="fontList" ref="menubar"></menu-bar>
</div>
</template>

<script>
import Epub from 'epubjs'
import TitleBar from '@/components/TitleBar'
import MenuBar from '@/components/MenuBar'
const DOWNLOAD_URL = '/static/2018_Book_AgileProcessesInSoftwareEngine.epub'
export default {
	data() {
		return {
			titleMenu: false,
			fontList: [
				{fontsize: 12},
				{fontsize: 14},
				{fontsize: 16},
				{fontsize: 18},
				{fontsize: 20},
				{fontsize: 22},
				{fontsize: 24},
			]
		};
	},
	components: {
		TitleBar,
		MenuBar
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
		},
		toggleTitleMenu() {
			this.titleMenu = !this.titleMenu
			if(!this.titleMenu) {
				this.$refs.menubar.hideSettingFont()
			}
			// if(this.titleMenu) {
			// 	this.titleMenu = false
			// } else {
			// 	this.titleMenu = true
			// }
			
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
	}
</style>