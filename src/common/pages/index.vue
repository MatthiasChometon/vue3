<script setup lang="ts">
const { t } = useI18n()
const $q = useQuasar()

const name = ref(null)
const age = ref(null)
const accept = ref(false)

function onSubmit() {
  if (accept.value !== true) {
    $q.notify({
      color: 'red-5',
      textColor: 'white',
      icon: 'warning',
      message: 'You need to accept the license and terms first',
    })
  }
  else {
    $q.notify({
      color: 'green-4',
      textColor: 'white',
      icon: 'cloud_done',
      message: 'Submitted',
    })
  }
}

function onReset() {
  name.value = null
  age.value = null
  accept.value = false
}
</script>

<template>
  {{ t('home') }}
  <div class="q-pa-md" style="max-width: 400px">
    <q-form class="q-gutter-md" @submit="onSubmit" @reset="onReset">
      <q-input
        v-model="name" filled label="Your name *" hint="Name and surname" lazy-rules
        :rules="[val => val && val.length > 0 || 'Please type something']"
      />

      <q-input
        v-model="age" filled type="number" label="Your age *" lazy-rules :rules="[
          val => val !== null && val !== '' || 'Please type your age',
          val => val > 0 && val < 100 || 'Please type a real age'
        ]"
      />

      <q-toggle v-model="accept" label="I accept the license and terms" />

      <div>
        <q-btn label="Submit" type="submit" color="primary" />
        <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm" />
      </div>
    </q-form>
  </div>
  <div h-full text-center flex select-none all:transition-400>
    <div ma>
      <div text-5xl fw100 animate-bounce-alt animate-count-infinite animate-duration-1s>
        unocss
      </div>
      <div op30 text-lg fw300 m1>
        The instant on-demand Atomic CSS engine.
      </div>
    </div>
  </div>
  <div absolute bottom-5 right-0 left-0 text-center op30 fw300>
    on-demand · instant · fully customizable
  </div>
</template>
