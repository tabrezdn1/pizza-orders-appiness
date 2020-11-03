<template>
  <div class="app">
    <div class="d-flex justify-content-center"><h1>Pizza Orders</h1></div>
    <div class="d-flex flex-column bd-highlight mb-3">
      <Order :orders="orders" />
    </div>
  </div>
</template>

<script>
import Order from "./components/Order.vue";

export default {
  name: "App",
  components: {
    Order,
  },
  data() {
    return {
      orders: [
        {
          id: 1,
          customerName: "Shaik Tabrez",
          orderItems: [
            { name: "One", cost: 10 },
            { name: "Two", cost: 20 },
          ],
          status: 0,
        },
        {
          id: 2,
          customerName: "Jeeva",
          orderItems: [
            { name: "One", cost: 10 },
            { name: "Two", cost: 20 },
          ],
          status: -1,
        },
        {
          id: 3,
          customerName: "Alex",
          orderItems: [
            { name: "One", cost: 10 },
            { name: "Two", cost: 20 },
          ],
          status: 1,
        },
        {
          id: 4,
          customerName: "John",
          orderItems: [
            { name: "One", cost: 10 },
            { name: "Two", cost: 20 },
          ],
          status: 0,
        },
      ],
    };
  },
};
</script>

<style>
.app{
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif
}
</style>
