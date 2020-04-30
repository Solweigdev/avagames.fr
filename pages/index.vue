<template>
  <div>
    <b-form @submit.prevent="submit">
      <b-form-input v-model="name" placeholder="Enter your name" required></b-form-input>
      <b-button type="submit" variant="primary">Submit</b-button>
    </b-form>
  </div>
</template>

<script>
import { mapMutations } from "vuex";

export default {
  name: "index",
  layout: "login",
  head: {
    title: "Avagames"
  },
  data: () => ({
    name: "",
    id: null
  }),

  methods: {
    ...mapMutations(["setUser"]),

    submit() {
      const user = {
        name: this.name,
        room: "default",
        id: 0
      };
      this.$socket.emit("createUser", user, data => {
        console.log("data", data);
        user.id = data.id;
        this.setUser(user);
        this.$router.push("/chat");
      });
    }
  }
};
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
