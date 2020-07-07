<template>
  <div class="about">
    <button @click="submitOrder">Order SLIK</button>
    <p v-for="(key, value) in Object.entries(customer)" :key="key">{{key}} : {{value}}</p>
  </div>
</template>

<script>
export default {
  name: 'Kafka',
  data() {
    return {
      customer: {},
    };
  },
  methods: {
    submitOrder() {
      alert('order submitted');
    },
  },
};
</script>
