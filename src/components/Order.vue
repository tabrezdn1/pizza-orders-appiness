<template>
  <div class="p-2">
    <!-- Each order renders here -->
    <b-card-group
      class="p-2 py-2"
      deck
      v-for="(order, orderIndex) in dataOrders"
      :key="orderIndex"
    >
      <!-- Render each card -->
      <b-card
        :header="'Customer : ' + order.customerName"
        :class="getDynamicClass(order.status)"
      >
        <!-- List of items ordered -->
        <b-list-group>
          <!-- Static Heading for items ordered -->
          <b-list-group-item
            >Items ordered
            <b-badge variant="primary" pill>{{
              order.orderItems.length
            }}</b-badge>
          </b-list-group-item>
          <!-- End of static Heading for items ordered -->

          <!-- Render items list from each order -->
          <b-list-group-item
            href="#"
            v-for="(orderItem, orderItemIndex) in order.orderItems"
            :key="orderItemIndex"
            >{{ orderItem.name }} : {{ orderItem.cost }}</b-list-group-item
          >
          <!-- Display subtotal from order id @invoke: getSubtotal() -->
          <b-list-group-item>
            Sub Total:
            <strong> {{ getSubtotal(order.id) }} </strong></b-list-group-item
          >
          <!-- End of items list from each order -->
        </b-list-group>

        <!-- Render footer -->
        <div>
          <h3>Status</h3>

          <!-- Conditional render based on status code  -->
          <template v-if="order.status == -1">
            Received
            <b-icon icon="three-dots" animation="throb" font-scale="2"></b-icon>
          </template>

          <template v-if="order.status == 0">
            Preparing
            <b-icon
              icon="arrow-clockwise"
              animation="spin-pulse"
              font-scale="2"
            ></b-icon>
          </template>

          <template v-if="order.status == 1">
            Ready to serve
            <b-icon icon="check-all" animation="throb" font-scale="2"></b-icon>
          </template>

          <!-- Update status on click @invoke: updateStatus() -->
          <button
            v-if="order.status == -1 || order.status == 0"
            class="btn btn-secondary btn-lg float-right"
            @click="updateStatus(order.id)"
          >
            Change Status
          </button>
        </div>
      </b-card>
    </b-card-group>
    <!-- End of each order -->
  </div>
</template>

<script>
export default {
  name: "Order",

  /**
   * @props - Array of Orders from app level
   */
  props: {
    orders: {
      type: Array,
      required: true,
    },
  },

  // Create a data property for array manipulation so we don't disturb the props.
  data() {
    return {
      dataOrders: [],
    };
  },

  // Assign props data to data property.
  mounted() {
    this.dataOrders = this.orders;
  },

  methods: {
    /**
     * @param id
     * @description Receives an id - Using the id finds the order and returns the total of all list items cost.
     */
    getSubtotal(id) {
      let order = this.dataOrders.find((item) => item.id == id);
      let items = order.orderItems;
      let subTotal = 0;

      for (let i = 0; i < items.length; i++) {
        subTotal += items[i]["cost"];
      }
      return subTotal;
    },

    /**
     * @param id
     * @description Receives an id - Using the id finds the order status and updates it back into the main dataOrders.
     */
    updateStatus(id) {
      let order = this.dataOrders.find((item) => item.id == id);
      if (order.status < 1) {
        for (let i = 0; i < this.dataOrders.length; i++) {
          if (this.dataOrders[i]["id"] == id) {
            this.dataOrders[i]["status"] += 1;
            return;
          }
        }
      }
    },

    /**
     * @param status
     * @description Receives order status - Based on the status returns a suitable class that will be applied dynamically.
     */
    getDynamicClass(status) {
      if (status == 1) {
        return "bg-success";
      } else if (status == 0) {
        return "bg-info";
      } else {
        return "bg-warning";
      }
    },
  },
};
</script>
