<template>
  <div>
    <table class="container">
      <tr>
        <th>#</th>
        <th>Name</th>
        <th>Age</th>
        <th>City</th>
        <th>Action</th>
      </tr>
      <tr v-for="user,index in role" :key="user.name">
        <td>{{index+1}}</td>
        <td>{{ user.name }}</td>
        <td>{{ user.age }}</td>
        <td>{{ user.city }}</td>
        <td>
          <button @click="$emit('delete', index)">Delete</button>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
    name:"studentApp",
    props: ["role"],
    emits:['delete'], 
};
</script>

<style lang="postcss" scoped>
</style>