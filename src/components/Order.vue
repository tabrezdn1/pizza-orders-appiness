<template>
  <div class="p-2 bd-highlight">
    <b-card-group
      class="p-2 py-2"
      deck
      v-for="(order, orderIndex) in dataOrders"
      :key="orderIndex"
    >
      <b-card
        :header="'Customer : ' + order.customerName"
        :class="getDynamicClass(order.status)"
      >
        <b-list-group>
          <b-list-group-item
            >Items ordered
            <b-badge variant="primary" pill>{{
              order.orderItems.length
            }}</b-badge></b-list-group-item
          >
          <b-list-group-item
            href="#"
            v-for="(orderItem, orderItemIndex) in order.orderItems"
            :key="orderItemIndex"
            >{{ orderItem.name }}</b-list-group-item
          >
          <b-list-group-item
            >Sub Total:
            <strong> {{ getSubtotal(order.id) }} </strong></b-list-group-item
          >
        </b-list-group>
        <div>
          <h3>Status</h3>
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
  </div>
</template>

<script>
export default {
  name: "Order",
  props: {
    orders: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      dataOrders: [],
    };
  },
  mounted() {
    this.dataOrders = this.orders;
  },
  methods: {
    getSubtotal(id) {
      let order = this.dataOrders.find((item) => item.id == id);
      let items = order.orderItems;
      let subTotal = 0;

      for (let i = 0; i < items.length; i++) {
        subTotal += items[i]["cost"];
      }
      return subTotal;
    },
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
