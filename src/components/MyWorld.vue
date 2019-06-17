<template>
  <div id="myworld">
    Hello, i am {{ name }}. <button @click="$emit('onClick')">{{ message }}</button>
    <ul>
      <li v-bind:key="list.text" v-for="list in lists"> {{ list.text }}</li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: 'MyWorld',
    props: {
      name: String,
      message: String,
      onClick: Function,
    },
    data: function() {
      return {
        lists: [
          { text: 1 },
          { text: 2 },
          { text: 3 }, 
        ],
        showMessage: true,
      };
    }
  }
</script>

<style>
</style>