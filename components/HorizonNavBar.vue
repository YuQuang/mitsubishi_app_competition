<template>
    <div class="sticky top-0 h-16 bg-[#7B92A6] dark:bg-[#4e478324]
                border-b-[1px] border-[#91a0ac] dark:border-[#5d5b70] flex justify-between px-10">
        <div class="py-3 flex gap-4">
            <UIcon name="i-solar-monitor-broken" width="40" height="40" dynamic />
            <div class="text-3xl text-white">
                Fake<span class="text-cyan-300 dark:text-cyan-400">Vans</span>
            </div>
        </div>
        <div class="py-3"> </div>
        <div class="py-4 flex gap-5 items-center">
            <div @click="selected = !selected">
                <UToggle
                on-icon="i-solar-sun-2-bold"
                off-icon="i-solar-moon-bold"
                v-model="computeColorMode"
                size="xl"
                color="yellow"
                />
            </div>
            <UButton
            icon="i-heroicons-pencil-square"
            size="sm"
            color="indigo"
            square
            variant="soft"
            />
        </div>
    </div>
</template>

<script setup lang="ts">
const colorMode = useColorMode()
const selected = ref(false)

const computeColorMode = computed({
    get(){
        if (selected.value) colorMode.preference = "light"
        else colorMode.preference = "dark"
        return selected.value
    },
    set(_: boolean){
        return _
    }
})
</script>