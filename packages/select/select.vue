<template lang="pug">
.zi-select-container(:class="[{ disabled, simple }, size && size]")
  select.zi-select(
    v-model="model"
    :class="{ disabled }"
    :form="form"
    :autocomplete="autocomplete"
    :autofocus="autofocus"
    :name="name"
    :disabled="disabled"
  )
    slot
  .arrow-box(v-if="!simple")
    down.arrow
</template>

<script>
import down from './down-icon'
import { validator } from '../utils'

export default {
  name: 'zi-select',

  components: { down },

  data: () => ({
    privateModel: undefined,
  }),

  props: {
    value: [String, Number, Boolean],
    size: {
      type: String,
      validator: validator.enums(['mini', 'small', 'medium']),
    },
    autocomplete: Boolean,
    autofocus: Boolean,
    disabled: Boolean,
    simple: Boolean,
    form: [String, Number],
    name: [String, Number],
  },

  computed: {
    model: {
      get() {
        return this.value === undefined ? this.privateModel : this.value
      },

      set(val) {
        this.privateModel = val
        this.$emit('input', val)
      },
    },
  },
}
</script>

<style lang="stylus" src="./select.styl"></style>
