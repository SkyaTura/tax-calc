<template>
  <v-layout align-center>
    <v-flex xs12 sm8 md6 class="flex-grow-1">
      <v-card class="flex-grow-1">
        <v-card-title class="headline">
          Insira os valores
        </v-card-title>
        <v-card-text>
          <v-text-field
            v-model="quantity"
            label="Quantidade"
            type="number"
          ></v-text-field>
          <v-currency-field
            v-model="value"
            v-bind="currency_config"
            label="Quantidade"
            type="number"
          ></v-currency-field>
        </v-card-text>
        <v-card-title class="headline">
          Resultado
        </v-card-title>
        <v-card-text>
          <div class="title">Débito</div>
          <div class="headline">R$ {{ debitValue }}</div>
          <div class="title">Crédito</div>
          <div class="headline">R$ {{ creditValue }}</div>
        </v-card-text>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
export default {
  data: () => ({
    quantity: 1,
    value: 0,
    debitTax: 0.0199,
    creditTax: 0.0474,
    currency_config: {
      decimal: ',',
      thousands: '.',
      prefix: 'R$ ',
      suffix: '',
      precision: 2,
      masked: false,
      allowBlank: false,
      min: Number.MIN_SAFE_INTEGER,
      max: Number.MAX_SAFE_INTEGER
    }
  }),
  computed: {
    total() {
      return this.quantity * this.value
    },
    debitValue() {
      return (this.total / (1 - this.debitTax)).toFixed(2)
    },
    creditValue() {
      return (this.total / (1 - this.creditTax)).toFixed(2)
    }
  }
}
</script>
