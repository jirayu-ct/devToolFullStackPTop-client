<script setup lang="ts">

const user_list_data = useState('user_list_data', () => [])

</script>

<template>
    <div class="h-screen w-screen flex">
        
        <div class="m-auto w-1/2">
            {{ user_list_data }}
            <DataCard />
        </div>

    </div>
</template>
