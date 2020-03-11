<template>
  <div>
    <v-card-widget enableActions :title="'Página Inicial'">
      <div slot="widget-header-action"></div>
      <div slot="widget-content">
        <v-row>
          <v-col cols="12">
            <v-data-table
              :headers="headers"
              :items="usuarios"
              :items-per-page="5"
              class="elevation-1"
            >
              <template v-slot:item.action="{ item }">
                <v-icon medium color="success" class="mr-2" @click="editItem(item)">edit</v-icon>
                <v-icon medium color="success" @click="deleteItem(item)">delete</v-icon>
              </template>
            </v-data-table>
          </v-col>
        </v-row>
      </div>
    </v-card-widget>

    <v-row justify="center">
      <v-dialog v-model="dialog" persistent max-width="600px">
        <template v-slot:activator="{ on }">
          <v-btn color="primary" dark v-on="on">Novo Usuário</v-btn>
        </template>
        <v-card>
          <v-card-title>
            <span class="headline">Cadastro de Usuário</span>
          </v-card-title>
          <v-card-text>
            <v-container>
              <v-row>
                <v-col cols="12" sm="6" md="4">
                  <v-text-field label="Nome do Usuário*" required></v-text-field>
                </v-col>
                <v-col cols="12">
                  <v-text-field label="Email*" required></v-text-field>
                </v-col>
                <v-col cols="12">
                  <v-text-field label="Password*" type="password" required></v-text-field>
                </v-col>
              </v-row>
              <input type="checkbox" id="checkbox" v-model="checked">
              <label for="checkbox">Ativo</label>
            </v-container>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="blue darken-1" text @click="dialog = false">Salvar</v-btn>
            <v-btn color="blue darken-1" text @click="dialog = false">Cancelar</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-row>
  </div>
</template>

<script>
// @ is an alias to /src
import VCardWidget from "@/components/VWidget";
import { RepositoryFactory } from "@/repositories/RepositoryFactory";
const usuarioRepo = RepositoryFactory.get("usuario");

export default {
  name: "home",

  data: () => ({
    headers: [
      {
        text: "Nome",
        align: "left",
        value: "nome"
      },
      { text: "Email", value: "email" },
      { text: "Status", value: "status" },
      { text: "", value: "action" }
    ],
    usuarios: []
  }),

  created() {
    usuarioRepo
      .getAll()
      .then(res => {
        this.usuarios = res.data;
      })
      .catch(console.error);
  },

  computed: {},

  methods: {}
};
</script>

<style>
</style>
