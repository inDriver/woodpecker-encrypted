<template>
  <div
    class="w-full border border-gray-200 py-1 px-2 rounded-md bg-white hover:border-gray-300 dark:bg-dark-gray-700 dark:border-dark-400 dark:hover:border-dark-800"
    :class="{ 'bg-gray-200 dark:bg-gray-600': disabled }"
  >
    <input
      v-if="lines === 1"
      v-model="innerValue"
      class="w-full bg-transparent text-color focus:outline-none focus:border-blue-400"
      :class="inputClass"
      :disabled="disabled"
      :type="type"
      :placeholder="placeholder"
    />
    <textarea
      v-else
      v-model="innerValue"
      class="w-full bg-transparent text-color focus:outline-none focus:border-blue-400"
      :class="inputClass"
      :disabled="disabled"
      :placeholder="placeholder"
      :rows="lines"
    />
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, toRef } from 'vue';

export default defineComponent({
  name: 'TextField',

  props: {
    modelValue: {
      type: String,
      default: '',
    },

    placeholder: {
      type: String,
      default: '',
    },

    type: {
      type: String,
      default: 'text',
    },

    lines: {
      type: Number,
      default: 1,
    },

    disabled: {
      type: Boolean,
    },

    inputClass: {
      type: String,
      default: '',
    },
  },

  emits: {
    // eslint-disable-next-line @typescript-eslint/no-unused-vars
    'update:modelValue': (_value: string): boolean => true,
  },

  setup: (props, ctx) => {
    const modelValue = toRef(props, 'modelValue');
    const innerValue = computed({
      get: () => modelValue.value,
      set: (value) => {
        ctx.emit('update:modelValue', value);
      },
    });

    return {
      innerValue,
    };
  },
});
</script>
