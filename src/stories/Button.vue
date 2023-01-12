<template>
  <button type="button" :class="classes" @click="onClick" :style="style">{{ label }}</button>
</template>

<script lang="ts">
import './button.css';
import {defineComponent, PropType} from 'vue';

type ButtonLabel = 'String1' | 'String2';

export default defineComponent({
  name: 'my-button',

  props: {
    label: {
      type: String as PropType<ButtonLabel>,
      required: true,
    },
    primary: {
      type: Boolean,
      default: false,
    },
    size: {
      type: String,
      default: 'medium',
      validator: function (value) {
        return ['small', 'medium', 'large'].indexOf(value) !== -1;
      },
    },
    backgroundColor: {
      type: String,
    },
  },

  computed: {
    classes() {
      return {
        'storybook-button': true,
        'storybook-button--primary': this.primary,
        'storybook-button--secondary': !this.primary,
        [`storybook-button--${this.size}`]: true,
      };
    },
    style() {
      return {
        backgroundColor: this.backgroundColor,
      };
    },
  },

  methods: {
    onClick() {
      this.$emit('onClick');
    },
  },
});
</script>
