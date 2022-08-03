<template>
  <div class="flex-1 bg-white h-full flex flex-col">
    <div class="w-full h-14 flex justify-end items-center border-b border-gray-200">
       <input type="text" v-model="searchTerm" id="input" placeholder="Search..." class="p-2 w-80 text-gray-900 bg-gray-50 rounded-md border border-gray-300 sm:text-xs mr-2">
    </div>
    <div>
        <p>
        <vue-good-table
            :columns="columns"
            :rows="rows"
            :search-options="{
                enabled: true,
                externalQuery: searchTerm
            }"
            :sort-options="{
                enabled: true,
            }"
        >
        </vue-good-table>
        </p>
    </div>
    </div>
</template>
<script>
import 'vue-good-table/dist/vue-good-table.css';
import { VueGoodTable } from 'vue-good-table';

export default {
    props: ['currentFile',
        'currentFileData',
        'tableColumns'],
    data () {
        return {
            columns: [],
            rows: [],
            searchTerm: '',
        }
    },
    watch: {
        currentFile: 'handleData'
    },
    components: {
        VueGoodTable
    },
    methods: {
        handleData(){
            if(this.currentFile === ''){
                this.columns = []
                this.rows = []
                return
            }
            this.columns = this.currentFileData[this.currentFile].header;
            let columnsObj = []
            this.columns.forEach(item => {
                columnsObj.push({label: String(item), field: String(item)}) 
            })
            this.columns = [...columnsObj]
            this.rows = this.currentFileData[this.currentFile].data
        }
    }   
}

</script>

<style scoped>
.full {
  width: 100%;
}
</style>