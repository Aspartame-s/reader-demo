<template>
	<transition name="slide-up">
		<div class="menu-wrapper" v-show="titleMenu">
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
	</transition>
</template>

<script>
export default {
	data() {
		return {
		};
	},
	props: {
		titleMenu: {
			type: Boolean,
			default: false
		}
	},
	methods: {},
	created() {},
	mounted() {}
};
</script>
<style lang="scss" scoped>
@import '../assets/styles/global';
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
</style>