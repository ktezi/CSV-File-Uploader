<template>
  <div class="bg-white w-80 border-r-2 border-gray-200">
    <div class="w-full h-14 flex justify-center items-center border-gray-200 border-b-2">
      <label class="button block w-80 text-white flex justify-center items-center font-bold bg-blue-500 sm:text-xs m-4 p-2">
        <input @change="onFileChange" class="hidden" type="file" accept=".csv"/>
          Import CSV 
      </label>
    </div>
    <div class="w-full h-14">
        <SideBarItem v-for="(ele, index) in this.fileList" :key="index" :onClick="handleClick" 
        class="flex justify-center items-center" :handleDelete="handleDelete" :filePath ="ele.path" :currentFile="currentFile">
            {{ele.name}}
        </SideBarItem>
    </div>
  </div>
</template>
<script>
export default{
    props: {
        currentFile: String,
        setCurrentFile:{
            type: Function
        },
        setCurrentFileData:{
            type: Function
        }
    },
    data() {
        return {
            fileList: [],
            tableData: {},
        }
    },
    methods: {
        createCSVObject(fileData, path) {
            const reader = new FileReader();
            reader.onload = (e) => {
                let jsonResult = e.target.result;
                let lines = jsonResult.split('\n');
                lines = lines.slice(0,-1);
                const header = lines[0].split(',');
                const data = lines.slice(1).map(ele => {
                    const tableFields = ele.split(',');
                    return Object.fromEntries(header.map((val,i) => [val, tableFields[i]]));
                });
                this.tableData[path] = { data: data, header: header};
                this.setCurrentFileData(this.tableData);
                this.setCurrentFile(path);
            }
            reader.readAsText(fileData);
        },
        onFileChange(e) {
            let files = e.target.files;
            if(!files.length) return;
            this.fileList.push({name: files[0].name, path: e.target.value});
            this.createCSVObject(files[0], e.target.value);
        },
        handleClick(filePath) {
            this.setCurrentFile(filePath);
        },
        handleDelete(filePath) {
            this.fileList = this.fileList.filter(ele => ele.path !== filePath)
            if(this.fileList.length !== 0){
                this.setCurrentFile(this.fileList[0].path)
            } else {
                this.setCurrentFile('')
            }
        }
    }
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