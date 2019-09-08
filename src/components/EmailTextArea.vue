<template>
  <v-sheet elevation="12" class="pa-12">
    <v-textarea
      :value="value"
      @input="$emit('input', $event)"
      :disabled="disabled"
      :clearable="clearable"
      :counter="counter ? counter : false"
      :filled="filled"
      :flat="flat"
      :hint="hint"
      :label="title"
      :loading="loading"
      :no-resize="noResize"
      :outlined="outlined"
      :placeholder="placeholder"
      :row-height="rowHeight"
      :rows="rows"
    ></v-textarea>
    <v-btn @click="$emit('clear')">Clear</v-btn>
  </v-sheet>
</template>
<script lang='ts'>
import Vue from 'vue';

export default Vue.extend({
  props: {
    title: String,
    disabled: Boolean,
    value: String,
  },
  data: () => ({
    autofocus: false,
    clearable: true,
    counter: 0,
    filled: false,
    flat: true,
    hint: 'Sent Emails',
    loading: false,
    noResize: true,
    outlined: true,
    placeholder: 'Enter 1 email per line...',
    rowHeight: 1,
    rows: 10,
  }),
});
</script>
