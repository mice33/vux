<template>
	<div class="vux-timeline">
		<ul>
			<slot></slot>
		</ul>
	</div>
</template>

<script>
export default {
  name: 'timeline',
  props: {
    color: String,
    isShowIcon: {
      type: Boolean,
      default: true
    }
  },
  methods: {
    setChildProps () {
      if (!this.$children) return
      const len = this.$children.length
      this.$children.forEach((child, index) => {
        child.isLast = index === len - 1
        child.isFirst = index === 0
      })
    }
  }
}
</script>

<style lang="less">
@import '../../styles/variable.less';

.vux-timeline {
  padding: 32px;
}

.vux-timeline > ul > li {
  list-style: none;
}

@vux-timeline: ~"vux-timeline";

.@{vux-timeline} {
  &-item {
    position:relative;
  }

  &-item-content {
    padding:0 0 48px 38.4px;
  }

  &-item-head, &-item-head-first {
    position:absolute;
    content:'';
    z-index:99;
    border-radius:99px;
  }

  &-item-head {
    width:20px;
    height:20px;
    left:2px;top:8px;
  }

  &-item-head-first {
    width:40px;
    height:40px;
    left:-8px;top:10px;
  }

  &-item-tail {
    position:absolute;
    content:'';
    height:100%;
    width:4px;
    left:10px;
    top:10px;
    background-color: @timeline-item-bg-color;
  }

  &-item-checked {
    width: 100%;
    position: absolute;
    left: 0;
    top: 0;
    width: 40px;
    height: 40px;

    &.weui-icon-success-no-circle::before {
      // font-size: 14px;
      .px2px(font-size, 28PX);
      position: absolute;
      left: 6px;
      top: 6px;
      margin: 0!important;
      color: #FFF;
    }
  }
}

.vux-timeline-item-color {
	background-color: @timeline-item-bg-color;
}

.vux-timeline-item-content {
  .px2px(font-size, 32PX);
}
</style>
