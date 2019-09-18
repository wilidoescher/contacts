<template>
  <q-dialog ref="dialog" @hide="onDialogHide">
    <q-card class="q-dialog-plugin" style="height: 800px">
      <div class="q-pa-md" style="max-width: 400px">
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
          />

          <q-input
            filled
            v-model="company"
            label="Empresa"
            hint
            lazy-rules
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
          />

          <q-input
            filled
            v-model="email"
            label="E-mail"
            hint
            lazy-rules
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
          >
            <template v-slot:prepend>
              <q-icon name="warning" />
            </template>
          </q-input>

          <div align="right">
            <q-btn flat label="Cancelar" color="primary" style="right: 105px" v-close-popup />
            <q-btn label="Limpar" type="reset" color="primary" flat class="q-ml-sm" />
            <q-btn label="Salvar" type="submit" color="primary" v-close-popup />
          </div>
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
      id: null,
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

 watch: {
   contato: {
      immediate: true,
      handler (val, oldVal) {
        if (val) {
          this.id = val.id
          this.name = val.nome
          this.surname = val.sobrenome
          this.company = val.empresa
          this.email = val.email
          this.charge = val.cargo
          this.phone = val.fone
          this.observation = val.observacoes
         
        }
      }
    }
  },


  created() {},
  props: ['contato'],

  methods: {
    onSubmit() {
      if (this.accept !== true) {
        this.$q.notify({
          color: "blue-8",
          textColor: "white",
          icon: "fas fa-exclamation-triangle",
          message: "Salvo!"
        })

        if(this.id){
           axios
            .put("http://localhost:3000/contatos/"+ this.id, {
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
        }
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
      console.log('aheu')
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
