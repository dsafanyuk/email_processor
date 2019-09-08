<template>
  <v-sheet elevation="12" class="pa-12">
    <v-card class="scroll" height="150">
      <v-card-text>
        <span v-for="(email, index) in emails" v-bind:key="index">
          {{email}}
          <br />
        </span>
      </v-card-text>
    </v-card>
    <v-btn @click="csvExport(emails)">EXPORT</v-btn>
  </v-sheet>
</template>
<script lang='ts'>
import Vue from 'vue';

export default Vue.extend({
  props: {
    title: String,
    emails: Array,
  },
  data: () => ({
    disabled: true,
    autofocus: false,
    counter: 0,
    filled: false,
    flat: true,
    hint: 'Sent Emails',
    loading: false,
    noResize: true,
    outlined: true,
    rowHeight: 1,
    rows: 10,
  }),
  methods: {
    csvExport(arrData: string[]) {
      let csvContent = 'data:text/csv;charset=utf-8,';
      csvContent += arrData.join('\n');

      const data = encodeURI(csvContent);
      const link = document.createElement('a');
      link.setAttribute('href', data);
      link.setAttribute('download', 'List of Unopened Emails.csv');
      link.click();
    },
  },
});
</script>

<style scoped>
.scroll {
  overflow-y: auto;
}
</style>
