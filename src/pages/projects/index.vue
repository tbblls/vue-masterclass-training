<script setup lang="ts">
import { supabase } from '@/lib/supabaseClient'
import { ref } from 'vue'
import type { Tables } from '../../../database/types'

const projects = ref<Tables<'projects'>[] | null>(null)

const getProjects = async () => {
  const { data, error } = await supabase.from('projects').select()

  if (error) {
    console.error('Error fetching projects:', error)
    return
  }
  projects.value = data || []
  console.log('Projects:', projects.value)
}

getProjects()
</script>

<template>
  <div>
    <h1>Projects page</h1>
    <RouterLink to="/">Home</RouterLink>
    <ul>
      <li v-for="project in projects" :key="project.id">
        {{ project.name }}
      </li>
    </ul>
  </div>
</template>
