<script setup lang="ts">
import { ref, defineEmits } from "vue";
import {
  IonCard,
  IonCardHeader,
  IonCardTitle,
  IonCardContent,
  IonItem,
  IonInput,
  IonSelect,
  IonSelectOption,
  IonButton,
} from "@ionic/vue";

const itemName = ref("");
const address = ref("");
const status = ref("В обработке");
const emit = defineEmits(["add-order"]);

const submitOrder = () => {
  emit("add-order", {
    itemName: itemName.value,
    address: address.value,
    status: status.value,
  });
  itemName.value = "";
  address.value = "";
  status.value = "В обработке";
};
</script>
<template>
  <ion-card>
    <ion-card-header>
      <ion-card-title>Добавить заказ</ion-card-title>
    </ion-card-header>
    <ion-card-content>
      <ion-item>
        <ion-input
          v-model="itemName"
          label="Название товара"
          required
        ></ion-input>
      </ion-item>
      <ion-item>
        <ion-input
          v-model="address"
          label="Адрес доставки"
          required
        ></ion-input>
      </ion-item>
      <ion-item>
        <ion-select v-model="status" label="Статус">
          <ion-select-option>В обработке</ion-select-option>
          <ion-select-option>В пути</ion-select-option>
          <ion-select-option>Доставлено</ion-select-option>
        </ion-select>
      </ion-item>
      <ion-button expand="full" @click="submitOrder">Добавить заказ</ion-button>
    </ion-card-content>
  </ion-card>
</template>
