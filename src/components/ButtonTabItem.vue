<template>
  <div class="button-tab-item-wrap"
       :class="wrapClass">
    <div class="button-tab-item"
         :class="classes"
         :style="styles"
         @click="itemClick">
      <div class="button-tab-item-bg"
           :style="bgStyles"></div>
      <div class="slot">
        <slot>{{ label }}</slot>
      </div>
    </div>
  </div>
</template>

<script>
  import { Vue, Component, Prop, Watch } from 'vue-property-decorator'

@Component
  export default class ButtonTabItem extends Vue {
    @Prop({ type: [String, Number], default: () => '' }) value
    @Prop({ type: [String, Number], default: () => '' }) label

    selected = false

    get wrapClass () {
        return {
            ['gutter-' + this.$parent.gutter]: +this.$parent.gutter,
            'gutter-0': !+this.$parent.gutter,
            ['col-' + this.$parent.column]: +this.$parent.column,
            flex: !this.$parent.column
        }
    }

    get classes () {
        return {
            selected: this.selected
        }
    }

    get styles () {
        return {
            color: this.selected ? this.$parent.activeColor : this.$parent.defaultColor
        }
    }

    get bgStyles () {
        return {
            background: this.selected ? this.$parent.activeBgColor : this.$parent.defaultBgColor,
            borderColor: this.selected ? this.$parent.activeBorderColor : this.$parent.defaultBorderColor
        }
    }

    itemClick () {
        // 如果是单选模式并且已经选中则不触发任何操作
        if (!this.$parent.multiple && this.selected) return

        if (this.$parent.multiple) {
            this.selected = !this.selected
        } else {
            this.selected = true
        }
        this.$parent.$emit('item-click', this.value)
    }

    @Watch('$parent.value', { immediate: true, deep: true })
    onValueChange () {
        if (this.$parent.multiple) {
            const value = this.$parent.value instanceof Array ? this.$parent.value : this.$parent.value.split(',')
            this.selected = value.find(item => item === this.value)
        } else {
            this.selected = this.$parent.value === this.value
        }
    }
  }
</script>

<style lang="scss" scoped>
@for $i from 1 through 100 {
    .gutter-#{$i} {
        padding-left: ($i / 2) + px;
        padding-right: ($i / 2) + px;
    }
}

@for $i from 1 through 24 {
    .button-tab-item-wrap.col-#{$i} {
        width: percentage(1 / $i);
        box-sizing: border-box;
    }
}

.button-tab-item-wrap {
    &.gutter-0 {
        &:first-child {
            .button-tab-item-bg {
                border-top-left-radius: 8px;
                border-bottom-left-radius: 8px;
            }
        }

        &:last-child {
            .button-tab-item-bg {
                border-top-right-radius: 8px;
                border-bottom-right-radius: 8px;
            }
        }

        &:not(:last-child) {
            .button-tab-item-bg {
                border-right: 0 none;
            }
        }
    }

    &:not(.gutter-0) {
        border-radius: 8px;
        .button-tab-item-bg {
            border-radius: 8px;
        }
    }

    &.flex {
        flex: 1;
    }
}

.button-tab-item {
    text-align: center;
    position: relative;
    box-sizing: border-box;
    flex: 1;
    display: -webkit-box;
    -webkit-box-align: center;
    -webkit-box-pack: center;

    .slot {
        position: relative;
        z-index: 99;
    }

    .button-tab-item-bg {
        position: absolute;
        width: 200%;
        height: 200%;
        border: 1px solid;
        box-sizing: border-box;
        -webkit-transform-origin: 0 0;
        transform-origin: 0 0;
        -webkit-transform: scale(0.5);
        transform: scale(0.5);
    }
}
</style>
