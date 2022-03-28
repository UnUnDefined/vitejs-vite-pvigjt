<script setup>
import { ref } from 'vue';

defineProps({
  id: Number,
  name: String,
  email: String,
  role: String,
  status: String,
});

// defineProps({
//   msg: String,
// });
const count = ref(0);
// don't forget to mount to app div
</script>

<template>
  <tr>
    <th scope="col">{{ id }}</th>
    <th scope="col">{{ name }}</th>
    <th scope="col">{{ email }}</th>
    <th scope="col">{{ role }}</th>
    <th scope="col">{{ status }}</th>
    <th scope="col">
      <button type="button" class="btn">Edit User</button>
    </th>
  </tr>
</template>

<style scoped>
a {
  color: #42b983;
}

.card-body {
  background-color: rgb(94, 217, 255);
}
</style>
