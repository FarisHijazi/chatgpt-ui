<script setup>
import {useEnableWebSearch} from "~/composables/states";

const menu = ref(false)
const enableWebSearch = useEnableWebSearch()

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
            icon="travel_explore"
            :color="enableWebSearch ? '' : 'grey'"
        ></v-icon>
      </v-btn>
    </template>

    <v-container>
      <v-card
          min-width="300"
          max-width="500"
      >
        <v-card-title>
          <span class="headline">{{ $t('webSearch') }}</span>
        </v-card-title>

        <v-divider></v-divider>

        <v-card-text>
          <v-switch
              v-model="enableWebSearch"
              inline
              hide-details
              color="primary"
              :label="$t('webSearch')"
          ></v-switch>
        </v-card-text>
      </v-card>
    </v-container>
  </v-menu>
</template>

<style scoped>

</style>