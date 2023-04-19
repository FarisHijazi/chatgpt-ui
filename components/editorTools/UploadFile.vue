<script setup>
const { $i18n } = useNuxtApp()
const dialog = ref(true)
const uploading = ref(false)
const file = ref(null)
const errorMsg = ref('')
const fileChanged = () => {
  errorMsg.value = ''
}
const upload = async () => {
  if (file.value === null) {
    return;
  }
  uploading.value = true
  const formData = new FormData()
  formData.append('file', file.value.files[0])
  const { data, error } = await useAuthFetch('/api/chat/upload/', {
    method: 'POST',
    body: formData,
  })
  if (error.value) {
    errorMsg.value = $i18n.t('Failed to upload file')
  } else {
    dialog.value = false
    console.log(data.value)
  }
  uploading.value = false
}

</script>

<template>
  <v-dialog
      v-model="dialog"
      width="auto"
  >
    <template v-slot:activator="{ props }">
      <v-btn
          v-bind="props"
          icon
      >
        <v-icon
            icon="description"
        ></v-icon>
      </v-btn>
    </template>

    <v-card
    >
      <v-card-title>
        <span class="headline">{{ $t('Insert file') }}</span>
      </v-card-title>

      <v-divider></v-divider>

      <v-card-text>
        {{ $t('Currently, only PDF files are supported.') }}
      </v-card-text>

      <v-card-text>
        <v-file-input
            ref="file"
            show-size
            accept=".pdf"
            clearable
            :loading="uploading"
            :disabled="uploading"
            :label="$t('Please select a PDF file')"
            :error-messages="errorMsg"
            @change="fileChanged"
        ></v-file-input>
        <div
            class="d-flex justify-center"
        >
          <v-btn
              color="primary"
              :loading="uploading"
              @click="upload"
          >{{ $t('Insert') }}</v-btn>
        </div>

      </v-card-text>
    </v-card>
  </v-dialog>
</template>

<style scoped>

</style>