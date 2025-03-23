<script setup lang="ts">
import { ref, onMounted, watch } from "vue";
import {
  IonApp,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
} from "@ionic/vue";
import OrderForm from "@/components/OrderForm.vue";
import OrderList from "@/components/OrderList.vue";

interface Order {
  id: number;
  itemName: string;
  address: string;
  status: string;
}

const orders = ref<Order[]>([]);

onMounted(() => {
  const savedOrders = localStorage.getItem("orders");
  if (savedOrders) {
    orders.value = JSON.parse(savedOrders);
  }
});

watch(
  orders,
  (newOrders) => {
    localStorage.setItem("orders", JSON.stringify(newOrders));
  },
  { deep: true }
);

const addOrder = (order: Order) => {
  orders.value.push({ ...order, id: Date.now() });
};
</script>

<template>
  <ion-app>
    <ion-header>
      <ion-toolbar>
        <ion-title>Список заказов</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content>
      <OrderForm @add-order="addOrder" />
      <OrderList :orders="orders" />
    </ion-content>
  </ion-app>
</template>

<style scoped></style>
