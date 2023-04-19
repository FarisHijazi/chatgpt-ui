<script setup>
import {useFrugalMode} from "~/composables/states";

const menu = ref(false)
const frugalMode = useFrugalMode()
</script>

<template>
  <v-menu
      v-model="menu"
      :close-on-content-click="false"
  >
    <template v-slot:activator="{ props }">
      <v-btn
          v-bind="props"
          icon
      >
        <v-icon
            icon="network_wifi_2_bar"
            :color="frugalMode ? '' : 'grey'"
        ></v-icon>
      </v-btn>
    </template>

    <v-container>
      <v-card
          min-width="300"
          max-width="500"
      >
        <v-card-title>
          <span class="headline">{{ $t('frugalMode') }}</span>
        </v-card-title>

        <v-divider></v-divider>

        <v-card-text>
          <p>{{ $t('frugalModeTip') }}</p>
          <v-switch
              v-model="frugalMode"
              inline
              hide-details
              color="primary"
              :label="$t('frugalMode')"
          ></v-switch>
        </v-card-text>
      </v-card>
    </v-container>
  </v-menu>
</template>

<style scoped>

</style>