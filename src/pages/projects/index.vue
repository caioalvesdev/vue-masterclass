<script setup lang="ts">
import { projectsQuey } from '@/utils/supaQueries';
import type { Projects } from '@/utils/supaQueries';
import { columns } from '@/utils/tableColumns/projectsColumns'

usePageStore().pageData.title = 'Projects'

const projects = ref<Projects | null>(null)

const getProjects = async () => {
  const { data, error, status } = await projectsQuey

  if(error) useErrorStore().setError({ error, customCode: status })

  projects.value = data
}

await getProjects()


</script>

<template>
  <DataTable
    v-if="projects"
    :columns="columns"
    :data="projects"
  />
</template>
