<template>
  <main>
    <!-- <v-container fluid class="main-content"> -->
      <v-layout row wrap>
        <v-flex xs12 sm4 offset-sm2 class="px-2 pt-5">
          <h5 class="pt-5">A tecnologia evolui.</h5>
          <p>A gente te ajuda a evoluir junto.</p>
        </v-flex>
        <v-flex xs12 sm4>
          <p class="text-sm-right"><img src="/images/minecraft.png" ></p>
        </v-flex>
        <v-flex xs12 sm8 offset-sm2 d-flex>
          <v-card id="course-list">
            <v-toolbar class="light-blue">
              <v-toolbar-title>Cursos</v-toolbar-title>
            </v-toolbar>
            <v-list three-line subheader>
                <v-list-tile v-for="course in courses" :key="course.code" :router="true" :to="{name: 'curso-code', params:{code: course.code}}">
                  <v-list-tile-avatar>
                    <img v-if="course.icon" :src="course.icon">
                    <v-icon v-if="!course.icon" class="grey white--text">folder</v-icon>
                  </v-list-tile-avatar>
                  <v-list-tile-content>
                    <v-list-tile-title>{{ course.name }}, com <strong>{{ course.teachers }}</strong></v-list-tile-title>
                    <v-list-tile-sub-title>{{ course.description }}</v-list-tile-sub-title>
                  </v-list-tile-content>
                </v-list-tile>
            </v-list>
          </v-card>
        </v-flex>
      </v-layout>
    <!-- </v-container> -->
  </main>
</template>

<script>

import AppApi from '~apijs'

export default {
  asyncData(ctx) {
    return AppApi.list_courses().then((response) => {
        return {courses: response.data}
    });
  },
  data(){
    return {
      courses: [],
    }
  },
  methods: {
  },
  head(){
    return {
      title: "evolutio - A tecnologia evolui. A gente te ajuda a evoluir junto.",
      meta: [
        {property: 'og:url', content: 'http://evolutio.io'},
        {property: 'og:type', content: 'website'},
        {property: 'og:title', content: 'evolutio - Aprenda tudo o que você vai usar no mundo real'},
        {property: 'og:description', content: 'O conteúdo com a qualidade que você precisa, em um só lugar.'},
        {property: 'og:image', content: 'http://evolutio.io/images/minecraft.png'},
      ]
    }
  },
}
</script>

<style scoped>
  /*.title {
    padding-left: 20px;
  }
  .main-content{
    max-width: 900px
  }*/
</style>
