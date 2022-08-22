<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      color="#e6e6eb"
      :clipped="clipped"
      hide-overlay
      absolute
      temporary
      app
    > 
      <v-list>
        <v-container>
        <v-img style="width: 150px; margin-left:-15px; margin: auto"  src="data:image/svg+xml;charset=US-ASCII,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20width%3D%22578.5%22%20height%3D%22221%22%20viewBox%3D%220%200%20578.5%20221%22%3E%3Cg%20fill-rule%3D%22evenodd%22%20clip-rule%3D%22evenodd%22%20fill%3D%22%23003B4C%22%3E%3Cpath%20d%3D%22M0%20197.4C0%20212.6%208.8%20221%2023.3%20221s23.3-8.4%2023.3-23.6v-66.2H31.4V198c0%206.5-2.6%209.7-8.1%209.7s-8.1-3.2-8.1-9.7v-66.8H0v66.2zM75%20219.7v-55.3h.2l19.4%2055.3h13.2v-88.5H94.1v50.6h-.2l-18.6-50.6h-14v88.5H75M137.7%20153c0-6.6%202-9.8%208.1-9.8s8.1%203.2%208.1%209.8v44.9c0%206.6-2%209.8-8.1%209.8s-8.1-3.2-8.1-9.8V153zm-15.2%2045.2c0%2012.5%207.4%2022.7%2023.3%2022.7s23.3-10.2%2023.3-22.7v-45.6c0-12.5-7.3-22.7-23.3-22.7-15.9%200-23.3%2010.2-23.3%2022.7v45.6zM516.5%20160.7v-6.5c0-13.2-7.4-24.3-22.5-24.3-15.9%200-23.3%2010.2-23.3%2022.7v45.6c0%2012.5%207.4%2022.7%2023.3%2022.7%2015.2%200%2022.5-10.2%2022.5-22.7V188h-15.2v10.7c0%205.7-1.8%208.9-7.3%208.9-6.1%200-8.1-3.2-8.1-9.8V153c0-6.6%202-9.8%208.1-9.8%203.9%200%207.3%203.2%207.3%2010.7v6.9h15.2v-.1zM276.4%20131.2v38.6h-16.1v-38.6h-15.2v88.5h15.2v-35.2h16.1v35.2h15.2v-88.5M342.6%20170l-7-38.8h-18.9l-16.3%2088.4h14.7l3.5-22.4c17.2-.7%2026.2-14.9%2024-27.2zM326%20148.9h.3l3.1%2020.4c1.1%207.1-2.7%2013.1-8.8%2015l5.4-35.4z%22%2F%3E%3Cpath%20d%3D%22M333.6%20196.3l3.6%2023.4h14.7l-2.4-13.2c-1.3-6.9-5.5-10.2-12.6-10.2h-3.3zM375.9%20219.7v-36.3h6.6c37.4%200%2037.4-52.2%200-52.2h-21.8v88.5h15.2zm0-76h5.9c18.2%200%2018.2%2027.2%200%2027.2h-5.9v-27.2z%22%2F%3E%3Cpath%20d%3D%22M460.5%20219.7v-13.3h-27.2v-26h19.6v-13.2h-19.6v-22.8h25.5v-13.2h-40.7v88.5h42.4M229.6%20160.7v-6.5c0-13.2-7.3-24.3-22.5-24.3-15.9%200-23.3%2010.2-23.3%2022.7v45.6c0%2012.5%207.4%2022.7%2023.3%2022.7%2015.2%200%2022.5-10.2%2022.5-22.7V188h-15.2v10.7c0%205.7-1.8%208.9-7.4%208.9-6.1%200-8.1-3.2-8.1-9.8V153c0-6.6%202-9.8%208.1-9.8%203.9%200%207.4%203.2%207.4%2010.7v6.9h15.2v-.1z%22%2F%3E%3Cg%3E%3Cpath%20d%3D%22M547.1%20153c0-3.2.4-7.2%203.5-8.9%202.7-1.4%207.2-1.4%209.7.4%203.4%202.4%202.9%207.4%202.9%2011.1V197.8c0%202.6-.1%205.6-1.9%207.7-2.1%202.5-6.3%202.7-9.3%201.9-5-1.3-5-6.7-5-11v-13.3-29.4c.1-.3.1-.5.1-.7zm-15.2%2045.2c0%204.8%201.1%209.8%203.9%2013.8%202.8%204.1%207.2%206.8%2012%208%2010.3%202.6%2023-.1%2028.1-10.2%202.8-5.4%202.6-11.3%202.6-17.1v-23.1-16.7c0-8.8-3.8-17.2-12.2-20.9-5.4-2.3-11.7-2.6-17.4-1.5-4.9%201-9.5%203.5-12.5%207.6-2.9%203.9-4.2%208.7-4.4%2013.5v45.5c-.1.4-.1.8-.1%201.1zM563.3%20123.5l-16.2%204.3v-9.1l16.2-4.4v9.2%22%2F%3E%3C%2Fg%3E%3C%2Fg%3E%3Cg%20fill%3D%22%23003B4C%22%3E%3Cpath%20d%3D%22M238.8%208.9c-32.4%2011.3-65.6%2050-59%2091.1h10.7c-1.2-4.3-1.7-8.9-1.7-13.5.1-34.4%2020.6-64.1%2050-77.6zM346.5%2034c-2.4-.1-4.8-.1-7.3%200-3.1-3.8-6.5-7.4-10.1-10.7C333.5%2012.2%20332.7.4%20314.7%200c13.3%201.7%2011.6%2014.4%204.8%2026.4-21.3%2037.8-74.6%2057.7-115.7%2058.6%2041.5%202%2098.6-16.1%20121.4-53.9.8-1.4%201.6-2.8%202.3-4.2%2011.4%208.7%2020.5%2020%2026.5%2033.1-3.2-8.6-7.7-16.6-13.1-23.8%201.6.1%203.2.3%204.7.5%2020.6%204%2018%2022.1%206.5%2034.7-8.9%209.7-23.5%2020-41.4%2028.5H340c8.7-6.7%2015.8-13.8%2021-20.8%2015.1-20.4%2014.9-43.4-14.5-45.1z%22%2F%3E%3C%2Fg%3E%3C%2Fsvg%3E"></v-img>
        </v-container>

        <v-list-item
          style="margin-top:1%"
          v-for="(item, i) in items"
          :key="i"
          color="primary"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon color="primary">{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title color="primary" v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar
      :clipped-left="clipped"
      fixed
      color="primary"
      app
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-spacer> </v-spacer>
         <v-toolbar-title>
         <v-img
            src="https://www.unochapeco.edu.br/static/data/portal/sites/banners/811.png"
            max-width="160px"
            style=" border-radius: 50px;
            ">
          </v-img>
          </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-menu
        open-on-hover
        offset-y
      >
        <template v-slot:activator="{ on, attrs }">
          <v-btn
            color="primary"
            height="100%"
            v-bind="attrs"
            v-on="on"
            outlined
            fab
            elevation="0"
          >
          <v-badge
            v-if="badge"
            dot
            color="red"
            overlap
          >
            <v-icon
              color="white"
            >
              mdi-bell
            </v-icon>
          </v-badge>
          <v-icon 
              v-if="!badge"
              color="white"
            >
              mdi-bell
            </v-icon>
          </v-btn>
        </template>
        <v-card>
          <v-card-text>
        <v-list>
          <v-list-item
            v-for="(item, index) in Notification"
            :key="index"
            link
            :to="item.link"
          >
            <v-list-item-title>{{item.title}}</v-list-item-title>
          </v-list-item>
        </v-list>
        </v-card-text>
        </v-card>
      </v-menu>
      <v-menu
        open-on-hover
        offset-y
      >
        <template v-slot:activator="{ on, attrs }">
          <v-btn
            color="primary"
            height="100%"
            v-bind="attrs"
            v-on="on"
            outlined
            elevation="0"
          >
          <v-row>
            <v-col>
              <v-avatar
                size="40"
              >
                <v-img
                  src="https://img.freepik.com/fotos-gratis/imagem-aproximada-em-tons-de-cinza-de-uma-aguia-careca-americana-em-um-fundo-escuro_181624-31795.jpg?w=2000"
                >
                </v-img>
              </v-avatar>
            </v-col>
            <v-col>
              <p style="color:white; margin-top: 15%;">
                  Arni
              </p>
            </v-col>
          </v-row>
          </v-btn>
        </template>
        <v-list>
          <v-list-item
            v-for="(item, index) in items2"
            :key="index"
            link
            :to="item.link"
          >
            <v-list-item-title>{{item.title}}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    <v-navigation-drawer
      v-model="rightDrawer"
      :right="right"
      temporary
      fixed
    >
      <v-list>
        <v-list-item @click.native="right = !right">
          <v-list-item-action>
            <v-icon light>
              mdi-repeat
            </v-icon>
          </v-list-item-action>
          <v-list-item-title>Switch drawer (click me)</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-footer
      :absolute="!fixed"
      app
    >
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data () {
    return {
      badge:true,
      clipped: false,
      drawer: false,
      fixed: false,
      Notification: [
        {title: 'socorro', data: 'Muito frio todays'}
      ],
      items2: [
        {title: 'Meus dados',link: "google.com"},
        {title: 'Sair', link: "google.com"}
        
      ],
      items: [
        {
          icon: 'mdi-book',
          title: 'Create',
          to: '/'
        }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'UNOCHAPECO'
    }
  }
}
</script>