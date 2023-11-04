<template>
  <v-container class="mt-15">
    <v-responsive class="mt-8">
      <h1>Your shopping cart</h1>
      <v-row class="mt-2">
        <v-col cols="12" md="9">
          <v-card class="mb-5 mr-2 ml-2 pl-2 pt-2">
            <v-row>
              <v-col cols="12" md="4">
                <b> Article</b>
              </v-col>
              <v-col cols="12" md="4">
                <b>Quantité</b>
              </v-col>
              <v-col cols="12" md="2">
                <b> Price</b>
              </v-col>
            </v-row>
            <v-row
              class="mb-2"
              v-for="(item, index) in shopping_cart"
              :key="index"
            >
              <v-col cols="12" md="4">
                <v-img
                  :width="100"
                  :height="50"
                  aspect-ratio="16/9"
                  cover
                  :src="item.image"
                ></v-img>
              </v-col>
              <v-col cols="12" md="4">
                <v-btn
                  color="#08AC0C"
                  variant="tonal"
                  @click="AddQuantity(item)"
                  >+</v-btn
                >
                &nbsp;
                <b>{{ item.quantity }}</b> &nbsp;
                <v-btn
                  color="#08AC0C"
                  variant="tonal"
                  @click="SousQuantity(item)"
                  >-</v-btn
                >
              </v-col>
              <v-col cols="12" md="2">
                {{ item.quantity * item.price }}
              </v-col>
              <v-col cols="12" md="2">
                <v-btn
                  color="error"
                  @click="RemoveFromCart(item)"
                  size="small"
                  variant="tonal"
                  icon="mdi-close-thick"
                ></v-btn>
              </v-col>
            </v-row>

            <v-row v-if="shopping_cart == null" class="m-5 p-5">
              <v-alert color="warning" variant="outlined">
                <template v-slot:title> Warning </template>

                Your shopping cart is empty
              </v-alert>
            </v-row>
          </v-card>
        </v-col>

        <v-col cols="12" md="3">
          <v-card class="mb-2 mr-5">
            <v-card-title
              >Totale cart :
              <b>
                {{ totale_price }}
              </b>
            </v-card-title>
            <v-card-text>
              <v-row align="center" justify="center" class="mt-5">
                <v-dialog width="500">
                  <template v-slot:activator="{ props }">
                    <v-btn v-bind="props" color="#08AC0C" variant="flat"
                      >Valider Commande</v-btn
                    >
                  </template>

                  <template v-slot:default="{ isActive }">
                    <v-card title="Livraison + Paiement">
                      <form>
    <v-text-field
      v-model="state.name"
      :error-messages="v$.name.$errors.map(e => e.$message)"
      :counter="10"
      label="Name"
      required
      @input="v$.name.$touch"
      @blur="v$.name.$touch"
    ></v-text-field>

    <v-text-field
      v-model="state.email"
      :error-messages="v$.email.$errors.map(e => e.$message)"
      label="E-mail"
      required
      @input="v$.email.$touch"
      @blur="v$.email.$touch"
    ></v-text-field>

    <v-select
      v-model="state.select"
      :items="items"
      :error-messages="v$.select.$errors.map(e => e.$message)"
      label="Item"
      required
      @change="v$.select.$touch"
      @blur="v$.select.$touch"
    ></v-select>

    <v-checkbox
      v-model="state.checkbox"
      :error-messages="v$.checkbox.$errors.map(e => e.$message)"
      label="Do you agree?"
      required
      @change="v$.checkbox.$touch"
      @blur="v$.checkbox.$touch"
    ></v-checkbox>

    <v-btn
      class="me-4"
      @click="v$.$validate"
    >
      submit
    </v-btn>
    <v-btn @click="clear">
      clear
    </v-btn>
  </form>
                    </v-card>
                  </template>
                </v-dialog>
              </v-row>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-responsive>
  </v-container>
</template>

<script lang="ts" setup>
import { ref } from "vue";

import { reactive } from 'vue'
  import { useVuelidate } from '@vuelidate/core'
  import { email, required } from '@vuelidate/validators'

  const initialState = {
    name: '',
    email: '',
    select: null,
    checkbox: null,
  }

  const state = reactive({
    ...initialState,
  })

  const items = [
    'Item 1',
    'Item 2',
    'Item 3',
    'Item 4',
  ]

  const rules = {
    name: { required },
    email: { required, email },
    select: { required },
    items: { required },
    checkbox: { required },
  }

  const v$ = useVuelidate(rules, state)

  function clear () {
    v$.value.$reset()

    for (const [key, value] of Object.entries(initialState)) {
      state[key] = value
    }
  }


const shopping_cart = ref([]);
shopping_cart.value = JSON.parse(localStorage.getItem("cart") || "null");

function RemoveFromCart(item: any) {
  const indexItem = shopping_cart.value.indexOf(item);
  shopping_cart.value.splice(indexItem, 1);
  localStorage.setItem("cart", JSON.stringify(shopping_cart.value));
}

const totale_price = ref();
function CalculeTotal() {
  totale_price.value = 0;
  if (shopping_cart.value != null) {
    for (let index = 0; index < shopping_cart.value.length; index++) {
      totale_price.value =
        totale_price.value +
        parseInt(shopping_cart.value[index].price) *
          parseInt(shopping_cart.value[index].quantity);
    }
  }
}

CalculeTotal();
function AddQuantity(item: any) {
  const indexItem = shopping_cart.value.indexOf(item);
  shopping_cart.value[indexItem].quantity =
    parseInt(shopping_cart.value[indexItem].quantity) + 1;
  localStorage.setItem("cart", JSON.stringify(shopping_cart.value));
  CalculeTotal();
}
function SousQuantity(item: any) {
  const indexItem = shopping_cart.value.indexOf(item);

  if (parseInt(shopping_cart.value[indexItem].quantity) > 0) {
    shopping_cart.value[indexItem].quantity =
      parseInt(shopping_cart.value[indexItem].quantity) - 1;
    localStorage.setItem("cart", JSON.stringify(shopping_cart.value));
  }
  CalculeTotal();
}
</script>
