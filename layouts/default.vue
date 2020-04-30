<template>
  <div>
    <h1>Users in room</h1>
    <b-list-group v-for="(u, index) in users" :key="`user-${index}`" @click.prevent>
      <b-list-group-item>
        {{u.name}}
        <span v-if="u.id === user.id">(moi)</span>
      </b-list-group-item>
    </b-list-group>
    <nuxt />
  </div>
</template>

<script>
import { mapState, mapMutations } from "vuex";

export default {
  sockets: {
    updateUsers(users) {
      this.updateUsers(users);
    },
    newMessage(msg) {
      this.newMessage(msg);
    }
  },
  computed: {
    ...mapState(["user", "users"])
  },
  middleware: "auth",
  methods: {
    ...mapMutations(["clearData", "updateUsers", "newMessage"]),

    exit() {
      this.$socket.emit("userLeft", () => {
        this.$router.push("/?message=leftChat");
        this.clearData();
      });
    }
  },
  created() {
    this.$socket.emit("joinRoom", this.user);
  }
};
</script>
