<!-- 
 * @Name：vusui-app-layer [load] 加载层
 * @Site：http://www.vusui.com | https://vusui.github.io
 * @Author：林攀
 * @License：MIT
 * @开发日期：2019-12-18
 -->
<template>
	<view class="vus-layer" :style="setLayerStyle">
		<view class="vus-layer-loading vus-layer-anim" :class="addAnim">
			<view class="vus-layer-close" v-if="options.closeBtn" @click="close">
				<view class="vli-close"></view>
			</view>
			<view class="vus-layer-padding" :class="{'is-noicon':options.icon==-1}">
				<block v-if="options.icon!=-1">
					<view class="vus-layer-loading-icon">
						<view :class="'vus-layer-loading-'+options.icon"></view>
					</view>
					<view class="vus-layer-content" v-if="options.content">{{options.content}}</view>
				</block>
				<view v-else class="vus-layer-content">{{options.content||'加载中...'}}</view>
			</view>
		</view>
	</view>
</template>

<script>
import Util from '../common/utils.js';
export default {
	name: 'vusMsg',
	data() {
		return {
			addAnim: ''
		}
	},
	computed: {
		options() {
			return this.$vusuiLayer.state.loading;
		},
		hideAnim() {
			return this.options.hide;
		},
		setLayerStyle() {
			return `z-index:${this.options.zIndex};`;
		},
		setIcon() {
			return typeof this.options.icon === 'object';
		},
		setContent() {
			return typeof this.options.content === 'object';
		}
	},
	created() {
		this.addAnim = this.options.anim !== -1 ? 'vus-layer-anim-'+this.options.anim : '';
		this.options.time <= 0 || setTimeout(() => {
			this.close();
		}, this.options.time)
	},
    methods: {
		close() {
			Util.close(this.options, this.$vusuiLayer);
		}
    },
	watch: {
		hideAnim(newVal) {
			if (this.options.outAnim !== -1 && newVal) {
				this.addAnim = 'vus-layer-anim-close-'+this.options.outAnim;
			}
		}
	}
}
</script>

<style></style>
