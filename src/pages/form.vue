<template>
    <div class="q-pa-md" style="max-width: 400px">

    <q-form
      @submit="onSubmit"
      @reset="onReset"
      class="q-gutter-md"
    >
      <q-icon name="person" />
      <q-input
        filled
        v-model="name"
        label="Nome"
        hint=""
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'Please type something']"
      />
      <q-icon name="" />
      <q-input
        filled
        v-model="name"
        label="Sobrenome"
        hint=""
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'Please type something']"
      />
      <q-icon name="house" />
      <q-input
        filled
        v-model="name"
        label="Empresa"
        hint=""
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'Please type something']"
      />
      <q-icon name="" />
      <q-input
        filled
        v-model="name"
        label="Cargo"
        hint=""
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'Please type something']"
      />
      <q-icon name="email" />
      <q-input
        filled
        v-model="name"
        label="E-mail"
        hint=""
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'Please type something']"
      />
      <q-icon name="phone" />
      <q-input
        filled
        v-model="name"
        label="Telefone"
        hint=""
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'Please type something']"
      />


      <div>
        <q-btn label="Submit" type="submit" color="primary"/>
        <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm" />
      </div>
    </q-form>

  </div>
</template>

<style>
</style>

<script>
import axios from 'axios'
import qs from 'qs'
import { Dialog } from 'quasar'

export default {
  name: 'Formulario',
  data () {
    return {
      name: null,
      surname: null,
      company: null,
      email: null,
      charge: null,
      phone: null,
      

      accept: false
    }
  },

  methods: {
    onSubmit () {
      if (this.accept !== true) {
        this.$q.notify({
          color: 'red-5',
          textColor: 'white',
          icon: 'fas fa-exclamation-triangle',
          message: 'You need to accept the license and terms first'
        })
      }
      else {
        this.$q.notify({
          color: 'green-4',
          textColor: 'white',
          icon: 'fas fa-check-circle',
          message: 'Submitted'
        })
      }
    },

    onReset () {
      this.name = null
      this.age = null
      this.accept = false
    }
  }
}
</script>
