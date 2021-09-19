<template>
  <ul>
    <li v-for="user in users" :key="user" @click="removeUser(user)">
      {{ user }}
    </li>
  </ul>

  <div>
    <input type="text" ref="userNameInput" />
    <button @click="addUser">add</button>
  </div>
</template>

<script>
export default {
  data() {
    return { users: ['shahrokh', 'hi', 'there', 'after', 'sam aleik'] };
  },
  methods: {
    addUser() {
      const newUser = this.$refs.userNameInput.value;
      this.users.unshift(newUser);
    },
    removeUser(user) {
      this.users = this.users.filter(usr => usr !== user);
    }
  }
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 1rem 0;
  padding: 0;
}
li {
  border: 1px solid #ccc;
  padding: 1rem;
}
</style>
