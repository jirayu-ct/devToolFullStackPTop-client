<template>
  <div class="min-h-screen bg-gray-50 text-gray-900">
    <!-- Header -->
    <header class="border-b bg-white/70 backdrop-blur sticky top-0 z-10">
      <nav class="container mx-auto flex items-center justify-between px-4 py-3">
        <NuxtLink to="/" class="font-semibold text-lg">MyProfile jirayu</NuxtLink>
        <ul class="flex gap-5 text-sm">
          <li><NuxtLink class="hover:text-blue-600" to="/">Home</NuxtLink></li>
          <li><NuxtLink class="hover:text-blue-600" to="/posts/1">Blog</NuxtLink></li>
          <li><NuxtLink class="hover:text-blue-600" to="/register">Register</NuxtLink></li>
          <li><NuxtLink class="hover:text-blue-600" to="/login">Login</NuxtLink></li>
        </ul>
      </nav>
    </header>

    <!-- Main -->
    <main class="container mx-auto px-4 py-8">
      <section class="rounded-2xl bg-white shadow">
        <!-- Toolbar -->
        <div class="flex flex-col sm:flex-row sm:items-center gap-3 p-4 border-b">
          <h1 class="text-xl font-semibold flex-1">Contacts</h1>
          <div class="relative w-full sm:w-80">
            <input v-model="search" type="text" placeholder="Search name, phone, email..." class="w-full rounded-md border px-3 py-2 pr-9 focus:outline-none focus:ring-2 focus:ring-blue-500" />
            <span class="absolute right-2 top-1/2 -translate-y-1/2 text-gray-400">⌕</span>
          </div>
        </div>

        <!-- Desktop Table -->
        <div class="hidden md:block">
          <table class="w-full table-auto">
            <thead class="bg-gray-50 text-left text-sm text-gray-600">
              <tr>
                <th class="px-4 py-3 w-16">ID</th>
                <th class="px-4 py-3">Name</th>
                <th class="px-4 py-3">Phone</th>
                <th class="px-4 py-3">Email</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(c, i) in filtered" :key="i" class="border-t hover:bg-gray-50">
                <td class="px-4 py-3 text-gray-600">{{ c.id }}</td>
                <td class="px-4 py-3 font-medium">{{ c.name }}</td>
                <td class="px-4 py-3">{{ c.phone }}</td>
                <td class="px-4 py-3 text-blue-600"><a :href="`mailto:${c.email}`">{{ c.email }}</a></td>
              </tr>
              <tr v-if="filtered.length === 0">
                <td colspan="4" class="px-4 py-6 text-center text-gray-500">No results</td>
              </tr>
            </tbody>
          </table>
        </div>

        <!-- Mobile Cards -->
        <div class="md:hidden divide-y">
          <div v-for="(c, i) in filtered" :key="`m-${i}`" class="p-4">
            <div class="flex items-center gap-2">
              <span class="inline-flex h-6 w-6 items-center justify-center rounded-full bg-gray-100 text-xs text-gray-700">{{ c.id }}</span>
              <p class="font-semibold">{{ c.name }}</p>
            </div>
            <p class="text-sm text-gray-600 mt-1">{{ c.phone }}</p>
            <a class="text-sm text-blue-600" :href="`mailto:${c.email}`">{{ c.email }}</a>
          </div>
          <div v-if="filtered.length === 0" class="p-6 text-center text-gray-500">No results</div>
        </div>
      </section>
    </main>

    <!-- Footer -->
    <footer class="py-8 text-center text-sm text-gray-500">
      {{ new Date().getFullYear() }} Contacts
    </footer>
  </div>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue'

type Contact = {
  id: number
  name: string
  phone: string
  email: string
}

const search = ref('')

const contacts = ref<Contact[]>([
  { id: 1, name: 'Alice Johnson', phone: '+66 81-234-5678', email: 'alice@example.com' },
  { id: 2, name: 'Bob Smith', phone: '+66 86-555-1122', email: 'bob@example.com' },
  { id: 3, name: 'Charlie Brown', phone: '+66 89-777-8899', email: 'charlie@example.com' },
  { id: 4, name: 'Diana Prince', phone: '+66 82-111-2233', email: 'diana@example.com' },
  { id: 5, name: 'Evan Lee', phone: '+66 85-333-4455', email: 'evan@example.com' }
])

const filtered = computed(() => {
  const q = search.value.trim().toLowerCase()
  if (!q) return contacts.value
  return contacts.value.filter(c =>
    [String(c.id), c.name, c.phone, c.email].some(v => v.toLowerCase().includes(q))
  )
})
</script>

<style scoped>
/* Keep it minimal; Tailwind handles most styling */
</style>