<template>
  <div class="q-pa-md">
    <q-layout view="lhh LpR lff" container style="height: 800px" class="shadow-5 rounded-borders">
      <q-header reveal class="bg-blue-10">
        <q-toolbar>
          <q-btn flat round dense icon="menu" />
          <q-toolbar-title>Contatos</q-toolbar-title>
        </q-toolbar>
      </q-header>

      <div class="q-pa-md">
        <q-table title="Treats" :data="data" :columns="columns" row-key="nome"></q-table>
      </div>

      <q-page-container>
        <q-page padding>
          <p v-for="n in 15" :key="n"></p>
          <q-page-sticky position="bottom-right" :offset="[18, 440]">
            <div class="q-pa-md q-gutter-sm">
              <q-item clickable @click.native="caminhoForm">
                <q-btn fab icon="add"  color="primary" />
              </q-item>
            </div>
          </q-page-sticky>
        </q-page>
      </q-page-container>
    </q-layout>
     
    <q-dialog ref="dialog" @hide="onDialogHide">
      <q-card class="q-dialog-plugin">
        
      </q-card>
    </q-dialog>

  </div>
</template>

<style>
</style>

<script>
import axios from 'axios'
import qs from 'qs'
import form from './form'

export default {
  name: 'Contatos',
  data () {
    return {
      columns: [
        {
          name: 'nome',
          required: true,
          label: 'Nome',
          align: 'left',
          field: row => row.nome,
          format: val => `${val}`,
          sortable: true
        },
        {
          numero: 'fone',
          required: true,
          label: 'Telefone',
          align: 'right',
          field: row => row.fone,
          format: val => `${val}`,
          sortable: true
        },
      ],
      data: []
    }
  },
  created() {
    const vm = this
    axios.get('http://localhost:3000/contatos')
    .then(function (response) {
      vm.data = response.data
    })
  },
  methods: {
    openDialog () {
      this.$q.dialog({
        component: Form,
        parent: this, 
        text: 'something'
      }).onOk(() => {
        console.log('OK')
      }).onCancel(() => {
        console.log('Cancel')
      }).onDismiss(() => {
        console.log('Called on OK or Cancel')
      })
    },
    showDialog () {
      this.$q.dialog({
        title: 'Alert<em>!</em>',
        message: '<em>I can</em> <span class="text-red">use</span> <strong>HTML</strong>',
        html: true
      }).onOk(() => {
        console.log('OK')
      }).onCancel(() => {
        console.log('Cancel')
      }).onDismiss(() => {
        console.log('I am triggered on both OK and Cancel')
      })
    },
    alert () {
      this.$q.dialog({
        title: 'Alert',
        message: 'Some message'
      }).onOk(() => {
        console.log('OK')
      }).onCancel(() => {
        console.log('Cancel')
      }).onDismiss(() => {
        console.log('I am triggered on both OK and Cancel')
      })
    },

    confirm () {
      this.$q.dialog({
        title: 'Confirm',
        message: 'Would you like to turn on the wifi?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        console.log('>>>> OK')
      }).onOk(() => {
        console.log('>>>> second OK catcher')
      }).onCancel(() => {
        console.log('>>>> Cancel')
      }).onDismiss(() => {
        console.log('I am triggered on both OK and Cancel')
      })
    },

    prompt () {
      this.$q.dialog({
        title: 'Prompt',
        message: 'What is your name?',
        prompt: {
          model: '',
          type: 'text'
        },
        cancel: true,
        persistent: true
      }).onOk(data => {
        console.log('>>>> OK, received', data)
      }).onCancel(() => {
        console.log('>>>> Cancel')
      }).onDismiss(() => {
        console.log('I am triggered on both OK and Cancel')
      })
    },

    caminhoForm() {
      this.$q.dialog({
        component: form,
        parent: this, 
        text: 'something',
      }).onOk(() => {
        console.log('OK')
      }).onCancel(() => {
        console.log('Cancel')
      }).onDismiss(() => {
        console.log('Called on OK or Cancel')
      })
    },
    show () {
      this.$refs.dialog.show()
    },

    hide () {
      this.$refs.dialog.hide()
    },
    onDialogHide () {
      this.$emit('hide')
    }
  }
}
</script>
