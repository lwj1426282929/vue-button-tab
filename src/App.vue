<template>
  <button-tab v-model="data">
    <button-tab-item value="1">1</button-tab-item>
    <button-tab-item value="2">2</button-tab-item>
    <button-tab-item value="3">3</button-tab-item>
  </button-tab>
</template>

<script>
  import { Vue, Component } from 'vue-property-decorator'
  import ButtonTab from './components/ButtonTab'
  import ButtonTabItem from './components/ButtonTabItem'
  
  @Component({
    components: { ButtonTab, ButtonTabItem }
  })
  export default class App extends Vue {
    data = '1'
  }
</script>
