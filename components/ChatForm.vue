<template>
  <div>
    <b-form-input ref="msg" @keydown.enter="send" v-model="text" placeholder="Votre message..."></b-form-input>
    <div class="mt-2">Value: {{ text }}</div>
  </div>
</template>

<script>
import { mapState } from "vuex";

export default {
  data: () => ({
    text: ""
  }),
  computed: {
    ...mapState(["user"])
  },
  methods: {
    send() {
      if (this.text.length) {
        console.log(this.text);
        this.$socket.emit(
          "createMessage",
          {
            text: this.text,
            id: this.user.id
          },
          data => {
            this.text = "";
          }
        );
      }
    }
  }
};
</script>

<style>
</style>