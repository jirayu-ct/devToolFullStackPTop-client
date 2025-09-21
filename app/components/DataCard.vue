<script setup lang="ts">

const user_list_data = useState('user_list_data', () => [])

const getData = async () => {
    const res = await fetch('http://localhost:4000/user-list')
    user_list_data.value = await res.json()
}

onMounted(async () => {
    await getData()
})

</script>

<template>
    <div class="border rounded-md p-4">
        <div class="flex flex-col gap-3">
            <h2 class="text-xl text-center font-semibold">User List</h2>
            <UTable :data="user_list_data" class="flex-1" />  
        </div>
    </div>
</template>
