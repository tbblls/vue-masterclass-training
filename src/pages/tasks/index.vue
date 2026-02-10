<script setup lang="ts">
import { supabase } from '@/lib/supabaseClient'
import { ref } from 'vue'
import type { Tables } from '../../../database/types'

const tasks = ref<Tables<'tasks'>[] | null>(null)

const getTasks = async () => {
  const { data, error } = await supabase.from('tasks').select()

  if (error) {
    console.error('Error fetching tasks:', error)
    return
  }
  tasks.value = data || []
  console.log('Tasks:', tasks.value)
}

getTasks()
</script>

<template>
  <div>
    <h1>Tasks page</h1>
    <RouterLink to="/">Home</RouterLink>
    <ul>
      <li v-for="task in tasks" :key="task.id">
        {{ task.name }}
      </li>
    </ul>
  </div>
</template>
