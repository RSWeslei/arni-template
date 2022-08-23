<template>
  <v-container>
    <v-row class="font mt-5">
      <v-col>
        <template>
          <v-card
            class="secondary rounded-lg pa-4"
            elevation="10"
          >
            <v-card-title class="fontBold display-1">
                Cursos Cadastrados
              <v-spacer></v-spacer>
              <v-text-field
                v-model="search"
                color="primary"
                append-icon="mdi-magnify"
                placeholder="Pesquisar"
                background-color="secondary"
                persistent-placeholder
                hide-details
                single-line
                outlined
                rounded
                dense
              ></v-text-field>
              <v-spacer></v-spacer>
              <v-btn
                class="mx-2"
                elevation="1"
                color="primary"
                fab
                small
                @click="dialog = !dialog"
              >
                <v-icon
                  color="white"
                >
                  mdi-plus
                </v-icon>
              </v-btn>
            </v-card-title>
            <v-data-table
              style="background-color:lightgrey"
              :headers="headers"
              :items="data"
              :page.sync="page"
              :search="search"
              :items-per-page="itemsPerPage"
              color="primary"
              :footer-props="{
                'items-per-page-text': 'Itens por página',
                
              }"
              hide-default-footer
              @page-count="pageCount = $event"
            >
              <template v-slot:item.actions="{ item }">
                <v-icon
                  small
                  class="mr-2"
                  @click="editar(item)"
                  color="primary"
                >
                  mdi-pencil
                </v-icon>
                <v-icon
                  small
                  @click="deletar(item)"
                  color="red"
                >
                  mdi-delete
                </v-icon>
              </template>
            </v-data-table>
            <v-divider></v-divider>
            <v-card-actions>
              <div 
                class="pt-6"
              >
                <v-autocomplete
                  v-model="itemsPerPage"
                  label="Itens"
                  color= "primary"
                  class="pr-4 ml-6"
                  style="width:100px;"
                  :items="autocomplete"
                  background-color="white"
                  item-value="name"
                  item-text="name"
                  outlined
                  dense
                  rounded
                ></v-autocomplete>
              </div>
            <v-spacer></v-spacer>
              <v-pagination
                v-model="page"
                :length="pageCount"
                style="ma"
                circle
                color="primary"
                :total-visible="5"
              >
              </v-pagination>
            </v-card-actions>
          </v-card>
        </template>
      </v-col>
    </v-row>
    <v-dialog
      v-model="dialog"
      max-width="850px"
    >
      <v-card 
        color="white" 
        class="pa-4 rounded-lg"
      >
        <v-card-title>
          <span class="fontBold headline">Cadastro de Universidades</span>
        </v-card-title>
        <v-row style="margin:auto">
          <v-col cols="7">
            <v-form v-model="valid">
              <v-container> 
                <v-row >
                  <v-text-field
                    outlined
                    label="Nome da universidade"
                    background-color="secondary"
                    class="custom-placeholer-color text-green"
                    placeholder="Nome da universidade"
                    :rules="rule"
                  ></v-text-field>
                </v-row>
                <v-row>
                  <v-text-field
                    outlined
                    label="Url do Site"
                    background-color="secondary"
                    color="primary"
                    placeholder="URL do site"
                    :rules="rule"
                  ></v-text-field>
                </v-row>
                <v-row>
                  <v-card-text class="fontBold mt-n6 ml-n3 body-1">
                    Termo&nbsp;de&nbsp;cooperação
                  </v-card-text>
                </v-row>
                <v-row
                  class="mt-n4"
                >
                  <v-col
                    class="ml-n2 body-2" 
                    cols="5"
                  >
                    <v-menu
                      v-model="date.menuInicio"
                      :close-on-content-click="false"
                      transition="scale-transition"
                      offset-y
                      max-width="290px"
                      min-width="auto"
                    >
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                          v-model="date.dateInicio"
                          label="Data inicial"
                          persistent-hint
                          append-icon="mdi-calendar"
                          readonly
                          :rules="rule"
                          outlined
                          dense
                          background-color="secondary"
                          v-bind="attrs"
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker
                        v-model="dataInicial"
                        locale="utc"
                        no-title
                        @input="date.menuInicio = false"
                      ></v-date-picker>
                    </v-menu>
                  </v-col>
                  <v-col
                    class="ml-n2 body-2" 
                    cols="5"
                  >
                    <v-menu
                      v-model="date.menuFim"
                      :close-on-content-click="false"
                      transition="scale-transition"
                      offset-y
                      max-width="300px"
                      min-width="auto"
                    >
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                          v-model="date.dateFim"
                          label="Data final"
                          persistent-hint
                          append-icon="mdi-calendar"
                          readonly
                          :rules="rule"
                          outlined
                          dense
                          background-color="secondary"
                          v-bind="attrs"
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker
                        v-model="dataFinal"
                        locale="utc"
                        no-title
                        @input="date.menuFim = false"
                      ></v-date-picker>
                    </v-menu>
                  </v-col>
                </v-row>
                <v-row>
                  <v-col>
                    <v-row>
                      <v-card-text 
                        class="fontBold mt-n8 ml-n3 body-1"
                      >
                      Observações</v-card-text>
                    </v-row>
                    <v-row>
                      <v-textarea
                        background-color="secondary"
                        outlined
                        v-model="description"
                      >
                      </v-textarea>
                    </v-row>
                  </v-col>
                </v-row>
              </v-container>
            </v-form>
          </v-col>
          <v-col cols="5">
            <v-container>
              <v-row >
                <v-autocomplete
                  outlined
                  placeholder="País"
                  label="País"
                  :rules="rule"
                  background-color="secondary"
                ></v-autocomplete>
              </v-row>
              <v-row>
                <v-container> 
                  <v-carousel height="200px" class="rounded-lg">
                    <v-carousel-item
                      v-for="image in images"
                      :key="image.url"
                      :src="image.url"
                    >
                    </v-carousel-item>
                  </v-carousel>
                </v-container>
              </v-row>
              <v-row>
                <v-file-input
                  background-color="secondary"
                  color="primary "
                  :rules="rule"
                  label="Enviar imagens"
                  prepend-icon=""
                  append-icon="mdi-paperclip"
                  outlined
                  dense
                  multiple
                >
                </v-file-input>
              </v-row>
              <v-row>
                <v-text-field
                  outlined
                  dense
                  :rules="rule"
                  background-color="secondary"
                  label="Latitude"
                  placeholder="Latitude"
                ></v-text-field>
              </v-row>
              <v-row>
                <v-text-field
                  outlined
                  dense
                  background-color="secondary"
                  label="Longitude"
                  :rules="rule"
                  placeholder="Longitude"
                ></v-text-field>
              </v-row>
            </v-container>
          </v-col>
        </v-row>
        <v-card-actions>
          <v-container >
            <v-row class="ml-12">
              <v-col
                cols="10"
                align="right"
              >
                <v-btn
                  outlined
                  color="red"
                  @click="dialog = false"
                >
                  Cancelar
                </v-btn>
              </v-col>
              <v-col
                align="right"
              >
                <v-btn
                  outlined
                  color="primary"
                  @click="dialog = false"
                >
                  Salvar
                </v-btn>
              </v-col>
            </v-row>
          </v-container>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-container>
</template>


<script>
export default {
  name: "create",
  data() {
    return {
      search: "",
      dialog: false,
      dataInicial: '',
      dataFinal: '',
      valid: false,
      description: '',
      date: {
        menuInicio: '',
        menuFim: '',
        dateInicio: '',
        dateFim: ''
      },
      images: [
        {
          url: 'https://www.estudarfora.org.br/wp-content/uploads/2020/06/Oxford_university_The_Queen27s_College_by_Fenlio-cccc.jpg',
        },
        {
          url: 'https://www.infoescola.com/wp-content/uploads/2014/02/universidade-faculdade.jpg'
        }
      ],
      headers: [
        { text: "Código do Curso", value: "id", align: 'center' },
        { text: "Nome do Curso", value: "name", align: 'center' },
        { text: "Nome do Coordenador", value: "idCoord", align: 'center' },
        {text: "", value: "actions"}
      ],
      data: [{ name: "Ciência da computação", id: 0, idCoord: "Forg" },{ name: "Ciência da computação", id: 1, idCoord: "Forg" },{ name: "Ciência da computação", id: 2, idCoord: "Forg" },{ name: "Ciência da computação", id: 2, idCoord: "Forg" },{ name: "Ciência da computação", id: 2, idCoord: "Forg" },{ name: "Ciência da computação", id: 2, idCoord: "Forg" },{ name: "Ciência da computação", id: 2, idCoord: "Forg" },{ name: "Ciência da computação", id: 2, idCoord: "Forg" },{ name: "Ciência da computação", id: 2, idCoord: "Forg" },{ name: "Ciência da computação", id: 2, idCoord: "Forg" },{ name: "Ciência da computação", id: 2, idCoord: "Forg" }],
      autocomplete: [{name: 5}, {name: 10}, {name: 15}, {name: 20}, {name:25}, {name:30}],
      page:1,
      pageCount: 10,
      itemsPerPage:5,
      rule:[
        a => !!a || 'Cadastro inválido'
      ]
    };
  },
  methods:{
    editar (item){
      console.log(item);
      this.$router.push({
        name: 'create',
        params: {item}
      })
    },
  },
  watch:{
    dataInicial (date) {
      if (!date) return null
      const [year, month, day] = date.split('-')
      return this.date.dateInicio =  `${day}/${month}/${year}`
    },
    dataFinal (date) {
      if (!date) return null
      const [year, month, day] = date.split('-')
      return this.date.dateFim =  `${day}/${month}/${year}`
    },
  }
};
</script>

<style
  scoped
>
.font {
  font-family:system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}
.fontBold {
  font-family:system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  font-weight: bold;
}

</style>