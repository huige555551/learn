<template>
  <button :class="_clas" :style="styl" :disabled="disabled" :type="htmlType" @click="clickHandler">
    <slot></slot>
  </button>
</template>
<script>
import {
  cssPrefix
} from '@/utils/variable'

import mixins from '@/utils/mixins'

export default {
  mixins: [mixins.base, mixins.button],
  computed: {
    _clas() {
      return [cssPrefix + 'btn', this.type ? (cssPrefix + 'btn-' + this.type) : '', this.clas]
    }
  },
  data() {
    return {
      cssPrefix
    }
  },
  methods: {
    clickHandler(e) {
      this.$emit('on-click', e)
    }
  }
}

</script>
<style lang="less">
@import '~@/styles/variable.less';
@import '~@/styles/mixins.less';
.@{css-prefix}{
    &btn{
      .button;
      height:2.6rem;
      position:relative;
      width:100%;
      box-sizing:border-box;
      background-color:#fff;
      border-radius:@border-radius-base;
      font-size: inherit;
      cursor: default;
      &:before{
        border:1px solid @border-color-base;
        box-sizing:border-box;
        width:200%;
        height:200%;
        position:absolute;
        left:-50%;
        top:-50%;
        transform:scale(0.5);
        content:'';
        border-radius:2*@border-radius-base;
      }
      &:active{
        box-shadow:1px 0 100px rgba(0,0,0,0.15) inset;
      }
      &-primary{
        background-color:@primary-color;
        color:#fff;
        &:before{
          border-color:@primary-color;
          display:none;
        }
      }
      &-warning{
        background-color:@warning-color;
        color:#fff;
        &:before{
          border-color:@warning-color;
          display:none;
        }
      }
      &-dashed{
        background-color:#fff;
        color:@primary-color;
        border:0;
        &:active{
          box-shadow:none;
        }
        &:before{
          border-color:@primary-color;
        }
      }
      .disabled;
    }
  }

</style>
