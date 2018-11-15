<template lang="html">
  <div :class="['input', {'is-not-valid' : validate === false}]">
    <label >{{ name }}</label>

    <input :type="type"
      :value="value"
      @input="onInput"
      :placeholder="placeholder"
      v-if="this.needMask ? false : true"
      >

    <the-mask mask="+380#########"
      :type="type"
      :value="value"
      @input.native="onInput"
      :masked="false"
      :placeholder="placeholder"
      v-else>
    </the-mask>
    <div class="input__error">
      {{ error }}
    </div>
  </div>
</template>

<script>

import {TheMask} from 'vue-the-mask';

export default {
  props: {
    name: String,
    type: String,
    placeholder: String,
    value: String,
    isValid: Boolean,
    needMask: {
      type: Boolean,
      default: false
    },
    mask: {
      type: [String, Array],
    },
    pattern: RegExp,
    error: String
  },
  data() {
    return {
      validate: true,
      data: ''
    }
  },
  created() {
    if (this.value.length) {
      this.data = this.value;
    }
  },
  methods: {
    onInput(e) {
      this.data = this.value;

      this.$emit('onChangeInput', {
        name: this.name,
        value: e.target.value,
        valid: this.pattern.test(e.target.value)
      });

      if (this.pattern.test(e.target.value)) {
         this.validate= true;
      } else {
        this.validate = false;
      }
    }
  },
  components: {
    TheMask
  }
}
</script>

<style lang="sass">

@import '@/assets/helpers/_variables.sass'

.input
  position: relative
  &.is-not-valid
    input
      border-color: $red

    .input__error
      display: block
      
  label
    display: block
    margin-bottom: 5px
    font-size: 15px
    font-weight: 700
    text-transform: capitalize

  input
    width: 100%
    border: 1px solid $gray
    min-height: 30px
    font-size: 14px
    padding: 0 10px
    border-radius: 5px
    transition: border-color .15s

  &__error
    display: none
    font-size: 10px
    line-height: 1
    position: absolute
    top: 100%
    margin-top: 3px
    left: 0
    color: $red

</style>
