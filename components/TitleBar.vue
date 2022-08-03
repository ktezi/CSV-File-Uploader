<template>
  <div class="fixed w-full bg-white border-gray-200 border-b-2 p-4">
    <div class="flex flex-row justify-between">
      <div class="flex flex-row">
        <Logo />
        <p class="flex flex-col font-bold"> 
          Tables & Stuff
          <span class="font-medium text-xs text-gray-500 italic">Import, Investigate, Repeat.</span>
        </p>
      </div>      
    </div>
  </div>
</template>
<script>

import Logo from '../components/Logo.vue';

export default {
  components: { Logo },
}


</script>
<style scoped>
.full {
  width: 100%;
}
.solution {
  width: 40rem;
  height: 35rem;
  background-size: contain;
}
</style>
