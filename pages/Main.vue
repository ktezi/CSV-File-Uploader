<template>
   <div class="wrapper">
        <title-bar />
        <div class="h-screen w-full flex top-20 fixed overflow-scroll">
            <side-bar :setCurrentFile="setCurrentFile" :setCurrentFileData="setCurrentFileData" :currentFile="currentFile"/>
            <data-table :currentFile="currentFile" :currentFileData="currentFileData" :tableColumns="tableColumns"/>
        </div>
   </div>
</template>

<script>

import TitleBar from '../components/TitleBar.vue';
import SideBar from '../components/SideBar.vue';
import DataTable from '../components/DataTable.vue';

export default {
  components:{ TitleBar, SideBar, DataTable },

  data(){
    return{
      currentFile: "",
      currentFileData: {},
    }
  },

  methods: {
    setCurrentFile(filePath) {
      this.currentFile = filePath;
    },
    setCurrentFileData(fileData) {
      this.currentFileData = fileData;
    },
  }
}
</script>
<style scoped>
.full {
  width: 100%;
}

.body {
  height: calc(100vh - 4rem);
}
</style>
