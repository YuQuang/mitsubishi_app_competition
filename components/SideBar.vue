<template>
    <div class="h-full px-3 py-4 overflow-y-auto bg-[#7B92A6] dark:bg-[#4e478324]
                flex flex-col justify-between border-r-[1px] border-[#a09eb3a5] dark:border-[#7b92a64f]">
        <UVerticalNavigation :links="links" :ui="{
            size: 'text-md',
            inactive: 'text-gray-500 dark:text-gray-200 hover:text-gray-900 dark:hover:text-white hover:before:bg-gray-50 dark:hover:before:bg-gray-800/50',
            active: 'text-gray-900 dark:text-white before:bg-gray-100 dark:before:bg-gray-800',
          }"/>
          <div class="flex flex-col gap-2">
            <div>
              
            </div>
            <div>
              <UAlert
                description="Still in developing"
                :avatar="{ src: '/images/winnie.jpeg' }"
                title="What's new?"
              />
            </div>
          </div>
    </div>
</template>

<script>
export default {
  data(){
    return {
      links: [
        [
          {
            label: 'Dashboard',
            icon: 'i-heroicons-home',
            to: '/'
          }, {
            label: 'Statics',
            icon: 'i-heroicons-chart-bar',
            to: '/statics'
          }, {
            label: 'Setting',
            icon: 'i-heroicons-cog-8-tooth',
          }
        ],[
          {
            label: 'History',
            icon: 'i-heroicons-clock-16-solid',
            to: '/history'
          }, {
            label: 'Logout',
            icon: 'i-heroicons-x-mark-16-solid'
          }
        ]
      ]
    }
  }
}
</script>