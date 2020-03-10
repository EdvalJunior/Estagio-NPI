<template>
  <div>
    <v-card-widget enableActions :title="'Página Inicial'">
      <div slot="widget-header-action">

      </div>
      <div slot="widget-content">
        <v-btn color="primary" dark dense app> Novo Usuário</v-btn>
        <v-row>
          <v-col cols="12">
            <v-data-table
                    :headers="headers"
                    :items="usuarios"
                    :items-per-page="5"
                    class="elevation-1"
            >
              <template v-slot:item.action="{ item }">
                    <v-icon medium="" color="success" class="mr-2" @click="editItem(item)">edit</v-icon>
                    <v-icon medium="" color="success" @click="deleteItem(item)">delete</v-icon>
              </template>
            </v-data-table>
          </v-col>
        </v-row>
      </div>
    </v-card-widget>
  </div>
</template>

<script>
// @ is an alias to /src
  import VCardWidget from "@/components/VWidget";
  import {RepositoryFactory} from "@/repositories/RepositoryFactory";
  const usuarioRepo = RepositoryFactory.get("usuario");

export default {
  name: 'home',

  data: () => ({
    headers: [
      {
        text: 'Nome',
        align: 'left',
        value: 'nome',
      },
      { text: 'Email', value: 'email' },
      {text: 'Status', value: 'status'},
      {text: '', value: 'action'}
    ],
    usuarios :[]
  }),

  created() {
    usuarioRepo.getAll().then(res => {
      this.usuarios = res.data;
    }).catch(console.error);
  },

  computed: {

  },

  methods: {

  }
}
</script>

<style>


</style>
