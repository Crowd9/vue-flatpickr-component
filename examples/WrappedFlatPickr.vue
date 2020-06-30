<template>
   <div class="form-group">
      <label>{{label}}</label>
      <flat-pickr
        class="form-control"
        :value="value"
        :config="config"
        @input="onInput"
        @on-change="handleChange"
      />
  </div>
</template>

<script>
import flatPickrComponent from '../src/index.js';

export default {
  name: 'WrappedFlatPickr',
  props: ['value', 'config', 'label'],
  componets: {
    'flat-pickr': flatPickrComponent
  },
  data: () => ({
    originalInputType: null
  }),
  created() {
    // for testing purposes only, please don't do this
    this.originalInputType = Array.isArray(this.value) ? 'array' : 'string'
  },
  methods: {
    onInput(dateStr) {
      const parsedValue = this.originalInputType === 'array'
        ? dateStr.split()
        : dateStr

      console.log('wrapped:inputEvt')
      this.$emit('input', parsedValue)
    },
    handleChange() {
      console.log('wrapped:changeEvt')
    }
  }
}
</script>

<style>

</style>
