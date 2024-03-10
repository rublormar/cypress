<template>
  <div class="container">
    <h1>Users</h1>
    <form @submit.prevent="addUser" class="user-form">
      <input v-model="newUser" placeholder="Add user" class="user-input" />
      <button type="submit" class="submit-btn">Add</button>
    </form>
    <ul class="user-list">
      <li v-for="(user, index) in users" :key="index" class="user-item">
        <input
          v-model="user.name"
          @change="updateUser(index)"
          class="user-input"
        />
          <button @click="deleteUser(index)" class="delete-btn">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const users = ref([{ name: "User 1" }, { name: "User 2" }]);
    const newUser = ref("");

    function addUser() {
      users.value.push({ name: newUser.value });
      newUser.value = "";
    }

    function updateUser(index) {
      // This will automatically update the user because of Vue's reactivity system
    }

    function deleteUser(index) {
      users.value.splice(index, 1);
    }

    return { users, newUser, addUser, updateUser, deleteUser };
  },
};
</script>

<style scoped>
.container {
  width: 100%;
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  box-sizing: border-box;
}

.user-form {
  display: flex;
  margin-bottom: 20px;
}

.user-input {
  flex-grow: 1;
  padding: 10px;
  margin-right: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.submit-btn,
.delete-btn {
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  background-color: #007bff;
  color: white;
  cursor: pointer;
}

.delete-btn {
  background-color: #dc3545;
}

.user-list {
  list-style-type: none;
  padding: 0;
}

.user-item {
  margin-bottom: 10px;
}
</style>