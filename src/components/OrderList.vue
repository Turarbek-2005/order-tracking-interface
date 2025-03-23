<script setup lang="ts">
import { defineProps } from "vue";
import { IonList, IonItem, IonLabel } from "@ionic/vue";

interface Order {
  id: number;
  itemName: string;
  address: string;
  status: string;
}

defineProps<{ orders: Order[] }>();
</script>
<template>
  <ion-list>
    <ion-item v-for="order in orders" :key="order.id">
      <ion-label>
        <h2>{{ order.itemName }}</h2>
        <p>
          {{ order.address }} - <strong>{{ order.status }}</strong>
        </p>
      </ion-label>
    </ion-item>
  </ion-list>
</template>
