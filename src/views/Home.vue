<template>
  <v-container>
    <v-row>
      <v-col>
        <EmailTextArea title="SENT EMAILS" v-model="sentEmails" v-on:clear="sentEmails = ''" />
      </v-col>
      <v-col>
        <EmailTextArea title="OPENED EMAILS" v-model="openedEmails" v-on:clear="openedEmails = ''" />
      </v-col>
    </v-row>
    <!-- <v-row align="center" justify="center">
      <v-btn
        color="green"
        @click="processData(sentEmailsArray,openedEmailsArray,unopenedEmails)"
      >Process</v-btn>
    </v-row>-->
    <v-row v-if="unopenedEmails.length > 0">
      <ReadOnlyTextArea title="OPENED EMAILS" v-bind:emails="unopenedEmails" />
    </v-row>
  </v-container>
</template>

<script lang="ts">
import Vue from 'vue';
import EmailTextArea from '../components/EmailTextArea.vue';
import ReadOnlyTextArea from '../components/ReadOnlyTextArea.vue';

export default Vue.extend({
  components: {
    EmailTextArea,
    ReadOnlyTextArea,
  },
  data: () => ({
    sentEmails: '',
    openedEmails: '',
  }),
  computed: {
    sentEmailsArray() {
      return this.sentEmails.split('\n');
    },
    openedEmailsArray() {
      return this.openedEmails.split('\n');
    },
    unopenedEmails() {
      const openedEmailsArray: string[] = this.openedEmailsArray;
      const sentEmailsArray: string[] = this.sentEmailsArray;
      const emails = sentEmailsArray.filter(
        (email: string) => !openedEmailsArray.includes(email),
      );
      return [...new Set(emails)];
    },
  },
});
</script>
