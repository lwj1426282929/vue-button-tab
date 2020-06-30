<template>
  <div>
    <button-tab v-model="data"
                :items="items">
    </button-tab>
    <button-tab v-model="data">
      <button-tab-item value="1">1</button-tab-item>
      <button-tab-item value="2">2</button-tab-item>
      <button-tab-item value="3">3</button-tab-item>
      <button-tab-item value="4">4</button-tab-item>
    </button-tab>
    <button-tab v-model="data"
                gutter="30">
      <button-tab-item value="1">1</button-tab-item>
      <button-tab-item value="2">2</button-tab-item>
      <button-tab-item value="3">3</button-tab-item>
      <button-tab-item value="4">4</button-tab-item>
    </button-tab>
    <button-tab v-model="data"
                :gutter="30"
                :column="2">
      <button-tab-item value="1">1</button-tab-item>
      <button-tab-item value="2">2</button-tab-item>
      <button-tab-item value="3">3</button-tab-item>
      <button-tab-item value="4">4</button-tab-item>
    </button-tab>
    <button-tab v-model="data"
                multiple
                gutter="30">
      <button-tab-item value="1">1</button-tab-item>
      <button-tab-item value="2">2</button-tab-item>
      <button-tab-item value="3">3</button-tab-item>
      <button-tab-item value="4">4</button-tab-item>
    </button-tab>
  </div>

</template>

<script>
  import { Vue, Component } from 'vue-property-decorator'
  import { ButtonTab, ButtonTabItem } from 'vue-button-tab'
  import 'vue-button-tab/lib/vue-button-tab.css'
  // import ButtonTab from './components/ButtonTab'
  // import ButtonTabItem from './components/ButtonTabItem'

@Component({
  components: { ButtonTab, ButtonTabItem }
})

  export default class App extends Vue {
  data = '1'

  items = [
    { label: '1', value: '1' },
    { label: '2', value: '2' },
    { label: '3', value: '3' },
    { label: '4', value: '4' }
  ]
  }
</script>

<style scoped>
/deep/.button-tab-item {
  margin-bottom: 20px;
}
</style>
