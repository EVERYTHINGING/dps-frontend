<template>
    <div class="uk-container uk-container-xsmall">
    <span class="uk-heading-small">
        <NuxtLink class="uk-button uk-button-text" to="/">
        <span uk-icon="arrow-left"></span> go back
        </NuxtLink>
    </span>

    <h2>{{ project.data.attributes.name }}</h2>
    <img
        :src="getStrapiMedia(project.data.attributes.image.data[0].attributes.url)"
        uk-cover
    />
    </div>
</template>

<script>
    import { getStrapiMedia } from '@/utils/media'
    import projectQuery from '@/apollo/queries/project'
    export default {
     data() {
        return {
          project: {},
        }
      },
      apollo: {
        project: {
          prefetch: true,
          query: projectQuery,
          variables() {
            return { id: this.$route.params.id }
          },
        },
      },
      computed: {
    
      },
      methods: {
        getStrapiMedia,
      },
      mounted(){
        console.log('data!', this.project)
      }
    }
</script>