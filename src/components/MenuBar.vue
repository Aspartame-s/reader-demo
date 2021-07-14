<template>
	<div class="menu-bar">
		<transition name="slide-up">
			<div class="menu-wrapper" v-show="titleMenu" :class="{'is-font-set' : isSettingfont || !titleMenu || isSettingTheme}">
				<div class="icon-wrapper">
					<span class="icon-menu icon"></span>
				</div>
				<div class="icon-wrapper">
					<span class="icon-progress icon"></span>
				</div>
				<div class="icon-wrapper" @click="showSetting(1)">
					<span class="icon-bright icon"></span>
				</div>
				<div class="icon-wrapper" @click="showSetting(0)">
					<span class="icon-a icon">A</span>
				</div>
			</div>
		</transition>
		<transition name="slide-up">
		<div class="setting-wrapper" v-show="isSettingfont">
			<div class="setting-font-size" v-if="showTag == 0">
				<div class="preview" :style="{fontSize: fontList[0].fontsize + 'px'}">A</div>
				<div class="select">
					<div class="select-wrapper" v-for="(item, index) in fontList" :key="index">
						<div class="line"></div>
						<div class="point-wrapper" @click="setFontSize(item.fontsize)">
							<div class="point" v-show="item.fontsize === defaultFontSize">
								<div class="small-point"></div>
							</div>
						</div>
						<div class="line"></div>
					</div>
				</div>
				<div class="preview" :style="{fontSize: fontList[fontList.length -1].fontsize + 'px'}">A</div>
			</div>
			<div class="setting-theme" v-else-if="showTag == 1">
				<div class="theme" v-for="(item, index) in styleList" :key="index" @click="setStyle(index)">
					<div class="theme-color" :style="{backgroundColor: item.style.body.color}"></div>
					<div class="theme-name">{{item.name}}</div>
				</div>
		</div>
		</div>
		</transition>
			
	</div>
</template>

<script>
export default {
	data() {
		return {
			isSettingfont: false,
			isSettingTheme: false,
			showTag: 0
		};
	},
	props: {
		titleMenu: {
			type: Boolean,
			default: false
		},
		fontList: Array,
		defaultFontSize: Number,
		styleList: Array,
		defaultTheme: Number
	},
	methods: {
		showSetting(tag) {
			this.isSettingfont = !this.isSettingfont
			this.showTag = tag
		},
		hideSettingFont() {
			this.isSettingfont = false
			this.isSettingTheme = false
		},
		setFontSize(fontSize) {
			this.$emit('setFontSize', fontSize)
		},
		settingTheme() {
			this.isSettingTheme = !this.isSettingTheme
		},
		setStyle(theme) {
			this.$emit('setTheme', theme)
		}
	},
	created() {},
	mounted() {}
};
</script>
<style lang="scss" scoped>
@import '../assets/styles/global';
.menu-bar {
	.menu-wrapper {
			position: absolute;
			bottom: 0;
			left: 0;
			width: 100%;
			height: px2rem(48);
			background-color: #fff;
			z-index: 102;
			display: flex;
			box-shadow: 0 px2rem(-8) px2rem(8) rgba(0,0,0,0.15);
			&.is-font-set {
				box-shadow: none;
			}
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
		.setting-wrapper {
			z-index: 101;
			position: absolute;
			bottom: px2rem(48);
			left: 0;
			width: 100%;
			height: px2rem(60);
			background-color: #fff;
			box-shadow: 0 px2rem(-8) px2rem(8) rgba(0,0,0,0.15);
			// display: flex;
			.setting-font-size {
				display: flex;
				height: 100%;
				.preview {
					flex: 0 0 px2rem(60);
					@include center
				}
				.select {
					display: flex;
					flex: 1;
					.select-wrapper {
						flex: 1;
						display: flex;
						align-items: center;
						&.select-wrapper:first-child {
							.line:first-child {
								border-top: none;
							}
						}
						&.select-wrapper:last-child {
							.line:last-child {
								border-top: none;
							}
						}
						.line {
							flex: 1;
							height: 0;
							border-top: px2rem(1) solid #ccc;
						}
						.point-wrapper {
							width: 0;
							height: px2rem(8);
							border-left: px2rem(1) solid #ccc;
							position: relative;
							.point {
								width: px2rem(20);
								height: px2rem(20);
								border: px2rem(1) solid #ccc;
								box-shadow: 0 px2rem(4) px2rem(4) rgba(0,0,0,0.15);
								border-radius: 50%;
								position: absolute;
								left: px2rem(-11);
								top: px2rem(-8);
								background-color: #fff;
								@include center;
								.small-point {
									width: px2rem(6);
									height: px2rem(6);
									border-radius: 50%;
									background-color: #000;
								}
							}
						}
					}
				}
			}
			.setting-theme {
				// z-index: 101;
				// position: absolute;
				// bottom: px2rem(48);
				// left: 0;
				// width: 100%;
				// height: px2rem(60);
				// background-color: #fff;
				// box-shadow: 0 px2rem(-8) px2rem(8) rgba(0,0,0,0.15);
				// display: flex;
				// justify-content: space-between;
				height: 100%;
				display: flex;
				.theme {
					flex: 1;
					margin: px2rem(10) px2rem(10);
					background-color: pink;
					font-size: px2rem(14);
					display: flex;
					justify-content: center;
					align-items: center;
					flex-direction: column;
					.theme-color {
						width: 100%;
						height: px2rem(10);
						margin-bottom: px2rem(5);
					}
				}
			}
		}
		
}

</style>