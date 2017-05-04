<template>
<div class="input-wrap">
	<input type="text" :placeholder="placeholder" :maxlength="normalizedMl" :value="value.val" @input="updateValue" @blur="onBlur" @focus="onFocus">
	<transition name="tip">
		<span class="valid-tip" v-show="tip.show">{{tip.content}}</span>
	</transition>
</div>
</template>


<script>
import ruleList from './rules'
export default {
	name: 'inputer',
	data() {
		return {
			tip: {
				show: false,
				content: ''
			},
			rules: ruleList
		}
	},
	props: {
		value: {
			type: Object,
			default: {
				val: '',
				valid: false
			}
		},
		tipNull: {
			type: String,
			default: '不能为空'
		},
		tipError: {
			type: String,
			default: '输入错误'
		},
		maxlength: {
			type: String,
			default: ''
		},
		placeholder: {
			type: String,
			default: ''
		},
		rule: {
			type: String,
			default: ''
		},
		ruleType: {
			type: String,
			default: ''
		},
		blur: {
			type: Boolean,
			default: true
		}
	},
	computed: {
		normalizedMl() {
			return isNaN(this.maxlength) ? '' : this.maxlength;
		},
		validRule() {
			return this.rule ? new RegExp(this.rule) : this.ruleType ? this.rules[this.ruleType] : false;
		}
	},
	methods: {
		updateValue(event) {
			if (event) {this.value.val = event.target.value;}
			this.value.valid = this.validate();
            this.$emit('input', this.value);
		},
		validate() {
			return !this.validRule ? true : this.validRule.test(this.value.val) ? true : false;
		},
		onBlur() {
			if (this.blur && !this.value.valid) {
				this.tip.content = this.value.val == '' ? this.tipNull : this.tipError;
				this.tip.show = true;
			}
		},
		onFocus() {
			this.tip.show = false;
		}
	},
	mounted() {
		this.updateValue();
	}
}
</script>


<style scoped>
.valid-tip{position:absolute; top:12px; right:1px; padding:0 2px; color:#f4574f; line-height:20px; font-size:12px; pointer-events:none; -webkit-transform:translate3d(0,0,0); transform:translate3d(0,0,0); -webkit-transition:.2s; transition:.2s;}
.tip-enter,
.tip-leave-active{opacity:0; -webkit-transform:translate3d(8px,0,0); transform:translate3d(8px,0,0);}
</style>