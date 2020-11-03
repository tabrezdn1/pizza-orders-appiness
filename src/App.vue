<template>
  <div class="pizza-order-app">
    <!-- Minimalistic Header -->
    <div class="d-flex justify-content-center">
      <h1>Pizza Orders</h1>
    </div>

    <!-- Render Order component -->
    <div class="d-flex flex-column bd-highlight mb-3">
      <Orders :orders="orders" />
    </div>
  </div>
</template>

<script>
// Import the Orders component
import Orders from "./components/Order.vue";

export default {
  name: "PizzaOrderApp",

  // Register as component
  components: {
    Orders,
  },

  // Data to be passed as prop to orders component
  /**
   * Object Prototype
   * @keys id, customerName, orderItems, status.
   * @id <Number> - Required in order to uniquely identify each order.
   * @customerName <String> - Name of the customer.
   * @orderItems <Array> - List of ordered items.
   * @status <Number> - Represents the status of the order. [ -1 : Received, 0 : Preparing, 1 : Ready to serve].
   */
  data() {
    return {
      orders: [
        {
          id: 1,
          customerName: "Shaik Tabrez",
          orderItems: [
            { name: "Chicken Toppings Pizza", cost: 280 },
            { name: "Sprite", cost: 40 },
          ],
          status: 0,
        },
        {
          id: 2,
          customerName: "Jeeva",
          orderItems: [
            { name: "Paneer Pizza", cost: 250 },
            { name: "Coke", cost: 50 },
            { name: "Ice-cream", cost: 150 },
          ],
          status: -1,
        },
        {
          id: 3,
          customerName: "Alex",
          orderItems: [
            { name: "Pepporani Pizza", cost: 300 },
          ],
          status: 1,
        },
        {
          id: 4,
          customerName: "John",
          orderItems: [
            { name: "Mixed Veg Pizza", cost: 210 },
            { name: "Salad", cost: 120 },
            { name: "Sprite", cost: 120 },
          ],
          status: 0,
        },
      ],
    };
  },
};
</script>

<style>
.pizza-order-app {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
}
</style>
