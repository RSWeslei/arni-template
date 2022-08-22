<template>
  <v-container>
    <v-row style="margin-top: 2%">
      <v-col>
        <template>
          <v-card
            style="background-color: lightgrey; border-radius: 10px; padding:2%"
            elevation="10"
          >
            <v-card-title style="font-family:system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif">
                <strong>
                  Cursos Cadastrados
                </strong>
              <v-spacer></v-spacer>
              <v-text-field
                v-model="search"
                append-icon="mdi-magnify"
                color="primary"
                rounded
                placeholder="forget"
                persistent-placeholder
                background-color="#d3d3d3 lighten-2"
                single-line
                outlined
                dense
                hide-details
              ></v-text-field>
              <v-spacer></v-spacer>
              <v-btn
                class="mx-2"
                fab
                elevation="1"
                small
                color="primary"
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
              
              <div style="width: 100px; padding-top:2%;">
                <v-autocomplete
                  
                  v-model="itemsPerPage"
                  label="Itens"
                  color= "primary"
                  style="width:100px; margin-left: -10%; padding-right:4%;"
                  :items="autocomplete"
                  outlined
                  background-color="white"
                  dense
                  rounded
                  item-text="name"
                  item-value="name"
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
      <v-card color="white" style="padding:3%">
        <v-card-title>
          <span class="cor">Cadastro de universidades</span>
        </v-card-title>
        <v-row style="margin:auto">
          <v-col cols="7">
            <v-container> 
              <v-row >
                <v-text-field
                  outlined
                  label="Nome da universidade"
                  background-color="#d3d3d3"
                  class="custom-placeholer-color text-green"
                  placeholder="Nome da universidade"
                ></v-text-field>
              </v-row>
              <v-row>
                <v-text-field
                  outlined
                  label="Url do Site"
                  background-color="#d3d3d3"
                  color="primary"
                  placeholder="URL do site"
                  
                ></v-text-field>
              </v-row>
              <v-row >
                <v-card-text style="font-size: 15px; margin-top: -25px;" class="cor">
                  Termo de cooperação
                </v-card-text>
              </v-row>
              <v-row>
                <v-col
                  style="font-size: 12px; color: primary;  margin-left: -10px;"
                  cols="5"
                >
                  <v-card-text 
                    style="font-size: 12px;" class="cor"
                  >
                    Data inicial
                  </v-card-text>
                  <v-text-field
                    background-color="#d3d3d3"
                    placeholder="10/10/2022"
                    append-icon="mdi-calendar"
                    outlined
                    dense
                  >
                  </v-text-field>
                </v-col>
                <v-col
                  style="font-size: 12px;  color: primary;"
                  cols="5"
                >
                    <v-card-text style="font-size: 12px;" class="cor">
                      Data final
                    </v-card-text>
                  <v-text-field
                    background-color="#d3d3d3"
                    placeholder="10/10/2023"
                    append-icon="mdi-calendar"
                    dense
                    outlined
                  >
                  </v-text-field>
                </v-col>
              </v-row>
              <v-row>
                <v-col>
                  <v-row style="color: primary">
                    <p class="cor"
                    >Observações</p>
                  </v-row>
                  <v-row>
                    <v-textarea
                      background-color="#d3d3d3"
                      outlined
                    >
                    </v-textarea>
                  </v-row>
                </v-col>
              </v-row>
            </v-container>
          </v-col>
          <v-col cols="5">
            <v-container>
              <v-row >
                <v-select
                  outlined
                  placeholder="País"
                  background-color="#d3d3d3"
                  class="custom-placeholer-color text-green"
                  persistent-placeholder
                ></v-select>
              </v-row>
              <v-row>
                <v-container> 
                  <v-carousel height="200px" style="border-radius:5%">
                    <v-carousel-item
                      src="https://www.estudarfora.org.br/wp-content/uploads/2020/06/Oxford_university_The_Queen27s_College_by_Fenlio-cccc.jpg"
                    >
                    </v-carousel-item>
                      <v-carousel-item
                      src="https://www.infoescola.com/wp-content/uploads/2014/02/universidade-faculdade.jpg"
                    >
                    </v-carousel-item>
                  </v-carousel>
                </v-container>
              </v-row>
              <v-row>
                <v-file-input
                  style="padding-right: 20px;"
                  outlined
                  background-color="#d3d3d3"
                  color="#1976d2"
                  multiple
                  label="Enviar imagens"
                >
                </v-file-input>
              </v-row>
              <v-row>
                <v-text-field
                  outlined
                  dense
                  background-color="#d3d3d3"
                  class="custom-placeholer-color text-green"
                  placeholder="Latitude"
                  persistent-placeholder
                ></v-text-field>
              </v-row>
              <v-row>
                <v-text-field
                  outlined
                  dense
                  background-color="#d3d3d3"
                  class="custom-placeholer-color text-green"
                  placeholder="Longitude"
                  persistent-placeholder
                ></v-text-field>
              </v-row>
            </v-container>
          </v-col>
        </v-row>
        <v-card-actions>
          <v-container >
            <v-row>
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
    };
  },
  methods:{
    editar (item){
      console.log(item);
      this.$router.push({
        name: 'create',
        params: {item}
      })
    }
  }
};
</script>

<style
  scoped
>
.cor {
  font-family:system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  font-weight: bold;
}

</style>