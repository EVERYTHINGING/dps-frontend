<template>
  <div class="uk-container uk-container-xsmall">
    <h1 class="uk-heading-small">
      <span class="uk-invisible">projects</span>
      <input
        v-model="query"
        class="uk-search-input"
        type="search"
        placeholder="Type to search"
      />
    </h1>

    <div
      v-for="project in filteredList"
      :key="project.id"
      class="
        uk-card uk-card-default uk-grid-collapse uk-child-width-1-2 uk-margin
      "
      uk-grid
    >
      <figure class="uk-flex-last uk-card-media-right uk-cover-container">
        <img
          :src="getStrapiMedia(project.attributes.image.data[0].attributes.url)"
          uk-cover
        />
      </figure>
      <div>
        <div class="uk-card-body uk-card-small">
          <h2 class="uk-card-title">{{ project.attributes.name }}</h2>
          <NuxtLink
            class="uk-button uk-button-text"
            :to="{ name: 'projects-id', params: { id: project.id } }"
          >
            See project
          </NuxtLink>
        </div>
      </div>
    </div>
    <div v-if="filteredList.length == 0" class="uk-heading-small">
      <p>No projects found</p>
    </div>
  </div>
</template>

<script>
import { getStrapiMedia } from '@/utils/media'
import projectsQuery from '@/apollo/queries/projects'
export default {
  data() {
    return {
      projects: [],
      query: '',
    }
  },
  apollo: {
    projects: {
      prefetch: true,
      query: projectsQuery,
    },
  },
  computed: {
    filteredList() {
      console.log(this.projects?.data);
      if (!this.projects?.data) return []
      return this.projects?.data?.filter((project) => {
        return project.attributes.name
          .toLowerCase()
          .includes(this.query.toLowerCase())
      })
    },
  },
  methods: {
    getStrapiMedia,
  },
}
</script>

<style scoped>
img {
  max-width: 300px;
}
</style>