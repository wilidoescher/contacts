<template>
  <q-dialog ref="dialog" @hide="onDialogHide">
    <q-card class="q-dialog-plugin">
      <div class="q-pa-md" style="max-width: 400px">
        <q-form @submit="onSubmit" @reset="onReset" class="q-gutter-md">
          <q-form @submit="onSubmit" @reset="onReset" class="q-gutter-md">
            <q-input
              filled
              v-model="name"
              label="Nome"
              hint
              lazy-rules
              :rules="[ val => val && val.length > 0 || 'Please type something']"
            >
              <template v-slot:prepend>
                <q-icon name="person" />
              </template>
            </q-input>

            <q-input
              filled
              v-model="surname"
              label="Sobrenome"
              hint
              lazy-rules
              :rules="[ val => val && val.length > 0 || 'Please type something']"
            />

            <q-input
              filled
              v-model="company"
              label="Empresa"
              hint
              lazy-rules
              :rules="[ val => val && val.length > 0 || 'Please type something']"
            >
              <template v-slot:prepend>
                <q-icon name="house" />
              </template>
            </q-input>

            <q-input
              filled
              v-model="charge"
              label="Cargo"
              hint
              lazy-rules
              :rules="[ val => val && val.length > 0 || 'Please type something']"
            />

            <q-input
              filled
              v-model="email"
              label="E-mail"
              hint
              lazy-rules
              :rules="[ val => val && val.length > 0 || 'Please type something']"
            >
              <template v-slot:prepend>
                <q-icon name="email" />
              </template>
            </q-input>

            <q-input
              filled
              v-model="phone"
              label="Telefone"
              mask="(##) ##### - ####"
              hint
              lazy-rules
              :rules="[ val => val && val.length > 0 || 'Please type something']"
            >
              <template v-slot:prepend>
                <q-icon name="phone" />
              </template>
            </q-input>

            <q-input
              filled
              v-model="observation"
              label="Observações"
              hint
              lazy-rules
              :rules="[ val => val && val.length > 0 || 'Please type something']"
            >
              <template v-slot:prepend>
                <q-icon name="warning" />
              </template>
            </q-input>

            <div>
              <q-btn label="Submit" type="submit" color="primary" />
              <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm" />
            </div>
          </q-form>
        </q-form>
      </div>
    </q-card>
  </q-dialog>
</template>

<style>
</style>

<script>
import axios from "axios"
import qs from "qs"
import { Dialog } from "quasar"

export default {
  name: "Formulario",
  data() {
    return {
      name: null,
      surname: null,
      company: null,
      email: null,
      charge: null,
      phone: null,
      observation: null,

      accept: false
    }
  },
  created() {},

  methods: {
    onSubmit() {
      if (this.accept !== true) {
        this.$q.notify({
          color: "blue-8",
          textColor: "white",
          icon: "fas fa-exclamation-triangle",
          message: "Salvo!"
        })
        axios
          .post("http://localhost:3000/contatos", {
            nome: this.name,
            sobrenome: this.surname,
            empresa: this.company,
            cargo: this.charge,
            email: this.email,
            fone: this.phone,
            observacoes: this.observation
          })
          .then(function(response) {
            console.log(response)
          })
          .catch(function(error) {
            console.log(error)
          })
      } else {
        this.$q.notify({
          color: "green-4",
          textColor: "white",
          icon: "fas fa-check-circle",
          message: "Submitted"
        })
      }
    },

    onReset() {
      this.name = null
      this.surname = null
      this.company = null
      this.email = null
      this.charge = null
      this.phone = null
      this.observation = null
      this.accept = false
    },
    show() {
      this.$refs.dialog.show()
    },
    hide() {
      this.$refs.dialog.hide()
    },

    onDialogHide() {
      this.$emit("hide")
    }
  }
}
</script>
