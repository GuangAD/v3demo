<template>
  <!-- 设置 css 变量 -->
  <div class="vr-flex" :class="classObject" :style="styleObject">
    <slot />
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, PropType } from "vue";
enum directionType {
  ROW = "row",
  COLUMN = "column",
  ROW_REVERSE = "row-reverse",
  COLUMN_REVERES = "column-reverse",
}
enum justifyContentType {
  SRART = "start",
  END = "end",
  CENTER = "center",
  AROUND = "around",
  BETWEEN = "between",
}
enum alignItemsType {
  SRART = "start",
  END = "end",
  CENTER = "center",
  BASELINE = "baseline",
  STRETCH = "stretch",
}
enum alignContentType {
  SRART = "start",
  END = "end",
  CENTER = "center",
  AROUND = "around",
  BETWEEN = "between",
  STRETCH = "stretch",
}
export default defineComponent({
  name: "VrFlex",
  props: {
    // 主轴
    direction: {
      type: String as PropType<directionType>,
      default: directionType.ROW,
    },
    // 是否允许换行
    wrap: {
      type: Boolean,
      default: true,
    },
    // 项目在主轴方向上
    justifyContent: {
      type: String as PropType<justifyContentType>,
      default: justifyContentType.SRART,
    },
    // 项目在交叉轴上如何对齐
    alignItems: {
      type: String as PropType<alignItemsType>,
      default: alignItemsType.STRETCH,
    },
    // 多根副轴线的对齐方式
    alignContent: {
      type: String as PropType<alignContentType>,
      default: alignContentType.STRETCH,
    },
    // row方向是否平分
    average: {
      type: Boolean,
      default: false,
    },
    // 元素之间的间隙大小（px）
    gap: {
      type: Number,
      default: 0,
    },
    // 行元素之间的间隙大小（px）
    rowGap: {
      type: [Number, String],
      default: 0,
    },
    // 列元素之间的间隙大小（px）
    columnGap: {
      type: [Number, String],
      default: 0,
    },
    // padding 大小
    wrapGap: {
      type: Number,
      default: 0,
    },
  },
  setup(props) {
    const classObject = computed(() => ({
      [`vr-flex-${props.direction}`]: true,
      [`vr-justify-${props.justifyContent}`]: true,
      [`vr-alignIt-${props.alignItems}`]: true,
      [`vr-alignCo-${props.alignContent}`]: true,
      "vr-flex-wrap": props.wrap,
      "vr-flex-average": props.average,
    }));
    const styleObject = computed(() => {
      const allGap = props.gap;
      const rowGap = props.rowGap;
      const colGap = props.columnGap;
      return {
        rowGap: `${props.rowGap}px`,
        columnGap: `${props.columnGap || allGap}px`,
        padding: `${props.wrapGap || allGap}px`,
        "--gap": `${props.columnGap || allGap}px`,
      };
    });
    return {
      classObject,
      styleObject,
    };
  },
});
</script>

<style lang="scss">
.vr-flex {
  display: flex;
  overflow: hidden;
  &.vr-flex-wrap {
    flex-wrap: wrap;
  }
  &.vr-flex-row {
    flex-direction: row;
    &.vr-flex-average > * {
      flex: 1;
      overflow: hidden;
    }
  }
  &.vr-flex-row-reverse {
    flex-direction: row-reverse;
    &.vr-flex-average > * {
      flex: 1;
      overflow: hidden;
    }
  }
  &.vr-flex-column {
    flex-direction: column;
    &.vr-flex-average {
      align-items: stretch;
      align-content: stretch;
      overflow: hidden;
    }
  }
  &.vr-flex-column-reverse {
    flex-direction: column-reverse;
    &.vr-flex-average {
      align-items: stretch;
      align-content: stretch;
      overflow: hidden;
    }
  }
  // 主轴
  &.vr-justify-start {
    justify-content: flex-start;
  }
  &.vr-justify-end {
    justify-content: flex-end;
  }
  &.vr-justify-center {
    justify-content: center;
  }
  &.vr-justify-between {
    justify-content: space-between;
  }
  &.vr-justify-around {
    justify-content: space-around;
  }
  // 副轴-单轴
  &.vr-alignIt-start {
    align-items: flex-start;
  }
  &.vr-alignIt-end {
    align-items: flex-end;
  }
  &.vr-alignIt-center {
    align-items: center;
  }
  &.vr-alignIt-baseline {
    align-items: baseline;
  }
  &.vr-alignIt-stretch {
    align-items: stretch;
  }

  // 副轴
  &.vr-alignCo-start {
    align-content: flex-start;
  }
  &.vr-alignCo-end {
    align-content: flex-end;
  }
  &.vr-alignCo-center {
    align-content: center;
  }
  &.vr-alignCo-between {
    align-content: space-between;
  }
  &.vr-alignCo-around {
    align-content: space-around;
  }
  &.vr-alignCo-stretch {
    align-content: stretch;
  }
  @for $i from 1 through 12 {
    & > .vr-grid-#{$i} {
      width: calc(100% * (#{$i} / 12) - #{"var(--gap)"}) !important;
    }
  }
  @for $i from 1 through 12 {
    & > .offset.vr-grid-offset-#{$i} {
      margin-left: 100% * ($i / 12) !important;
    }
  }
  .fill {
    flex: 1;
    overflow: hidden;
  }
  .unshrink {
    flex-shrink: 0;
  }
  .self-top {
    align-self: flex-start;
  }
  .self-center {
    align-self: center;
  }
  .self-bottom {
    align-self: flex-end;
  }
  .self-baseline{
    align-self: baseline;
  }
  .self-stretch{
    align-self: stretch;
  }
}
.full-width {
  width: 100%;
}
.full-height {
  height: 100%;
}
.text-center {
  text-align: center;
}
.text-right {
  text-align: right;
}
.one-line {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.two-line {
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 2;
}
</style>
