<template>
   <div @click="onClick(filePath)" class="w-full h-10 flex justify-between items-center cursor-pointer p-4">
    <div class="flex justify-between items-center">
      <img class="mr-2 h-5" src="../assets/fileIcon.png" />
      <p class="font-bold">
        <slot ></slot>
      </p>
    </div>      
      <img @click="handleDelete(filePath)" :src="trashIcon" @mouseenter="hover = true" @mouseleave="hover = false" />
  </div>
</template>
<script>

import trashIcon from "../assets/trashIcon.png";

export default {
    props: {
        currentFile: String,
        filePath: String,
        onClick: {
            type: Function
        },
        handleDelete: {
            type: Function
        }
    },
    data() {
        return {
            trashIcon: trashIcon
        }
    },
}
</script>
<style scoped>
.full {
  width: 100%;
}
</style>
