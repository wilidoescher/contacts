<template>
  <div class="q-pa-md">
    <q-layout view="lhh LpR lff" container style="height: 500px" class="shadow-5 rounded-borders">
      <q-header reveal class="bg-blue-10">
        <q-toolbar>
          <q-btn flat round dense icon="menu" />
          <q-toolbar-title>Contatos</q-toolbar-title>
        </q-toolbar>
      </q-header>

      <div class="q-pa-md">
        <div class="q-pa-md">
          <q-table
            title="Treats"
            :data="data"
            :columns="columns"
            row-key="id"
            :filter="filter"
            :loading="loading"
            selection="multiple"
            :selected.sync="selected"
          >
            <template v-slot:top>Top</template>
            <template v-slot:top-row>
              <q-tr>
                <q-td colspan="100%">Contatos</q-td>
              </q-tr>
            </template>
            
            <template v-slot:top>
              <q-btn
                class="on-right"
                flat
                dense
                color="primary"
                :disable="loading"
                label="Remover"
                @click="removeRow"
              />
              <q-space />
              <q-input borderless dense debounce="300" color="primary" v-model="filter">
                <template v-slot:append>
                  <q-icon name="search" />
                </template>
              </q-input>
            </template>
          </q-table>
        </div>
      </div>

      <q-page-container>
        <q-page padding>
          <p v-for="n in 15" :key="n"></p>
          <q-page-sticky position="bottom-right" :offset="[18, 18]">
            <div class="q-pa-md q-gutter-sm">
              <q-item clickable @click.native="caminhoForm">
                <q-btn fab icon="add" color="primary" />
              </q-item>
            </div>
          </q-page-sticky>
        </q-page>
      </q-page-container>
    </q-layout>

    <q-dialog ref="dialog" @hide="onDialogHide">
      <q-card class="q-dialog-plugin"></q-card>
    </q-dialog>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
import qs from "qs";
import form from "./form";

export default {
  name: "Contatos",
  data() {
    return {
      loading: false,
      filter: "",
      rowCount: 10,
      selected: [],
      columns: [
        {
          name: "nome",
          required: true,
          label: "Nome",
          align: "left",
          field: row => row.nome,
          format: val => `${val}`,
          sortable: true
        },
        {
          numero: "fone",
          required: true,
          label: "Telefone",
          align: "right",
          field: row => row.fone,
          format: val => `${val}`,
          sortable: true
        }
      ],
      data: []
    }
  },
  created() {
    this.gridRefresh()
  },
  methods: {
    caminhoForm() {
      this.$q
        .dialog({
          component: form,
          parent: this,
          text: "something"
        })
        .onOk(() => {})
        .onCancel(() => {})
        .onDismiss(() => {
          this.gridRefresh()
        })
    },
    show() {
      this.$refs.dialog.show()
    },

    hide() {
      this.$refs.dialog.hide()
    },
    onDialogHide() {
      this.$emit("hide")
    },
    gridRefresh() {
      const vm = this
      axios.get("http://localhost:3000/contatos").then(function(response) {
        vm.data = response.data
      })
    },
    gridDelete() {
      axios
        .delete("http://localhost:3000/contatos")
        
        .then(function(response) {
          // handle success
          console.log(response)
        })
        .catch(function(error) {
          // handle error
          console.log(error)
        })
        .finally(function() {
          // always executed
        })
    },

    removeRow() {
      this.loading = true
      for (let select = 0; select < array.length; index++) {
        const element = array[select]
        console.log(array[select])
        
      }
    }
  }
}
</script>
