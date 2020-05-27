<template>
  <div :class="['button-tab', 'clear-gutter-' + gutter]">
    <slot>
      <button-tab-item v-for="(item, index) in items"
                       :key="index"
                       :value="item.value"
                       :label="item.label"></button-tab-item>
    </slot>
  </div>
</template>

<script>
  import { Vue, Component, Model, Prop } from 'vue-property-decorator'
  import ButtonTabItem from './ButtonTabItem'

  @Component({
    components: { ButtonTabItem }
  })
  export default class ButtonTab extends Vue {
    @Model('change', { type: [String, Number, Array], default: '' }) value

    @Prop({ type: Boolean, default: () => false }) multiple
    @Prop({ type: Number, validator: (val) => { return val >= 0 && val <= 24 } }) column
    @Prop({ type: [Number, String], validator: (val) => { return val >= 0 && val <= 100 }, default: () => 0 }) gutter
    @Prop({ type: String, default: () => '#999999' }) defaultColor
    @Prop({ type: String, default: () => '#FFFFFF' }) activeColor
    @Prop({ type: String, default: () => '#FFFFFF' }) defaultBgColor
    @Prop({ type: String, default: () => '#2482FC' }) activeBgColor
    @Prop({ type: String, default: () => '#2482FC' }) defaultBorderColor
    @Prop({ type: String, default: () => '#2482FC' }) activeBorderColor
    @Prop({ type: Array, default: () => [] }) items

    created () {
      this.$on('item-click', this.toggleSelected)
    }

    toggleSelected (val) {
      const children = this.$children
      // 多选模式
      if (this.multiple) {
        const value = []
        for (const child of children) {
          if (child.selected) value.push(child.value)
        }
        this.$emit('change', value)
        this.$emit('on-item-click', value)
      } else { // 单选模式
        for (const child of children) {
          child.selected = child.value === val
        }
        this.$emit('change', val)
        this.$emit('on-item-click', val)
      }
    }
  }
</script>

<style lang="scss" scoped>
.button-tab {
    display: flex;
    flex-wrap: wrap;
}

@for $i from 1 through 100 {
    .clear-gutter-#{$i} {
        margin-left: -($i / 2) + px;
        margin-right: -($i / 2) + px;
    }
}
</style>
