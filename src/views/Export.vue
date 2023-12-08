<template>
  <div class="export-excel">
    <el-button size="small" type="primary" @click="exportExcelByTable">表格导出</el-button>
    <!-- 创建表格-->
    <el-table ref="table" :data="tableData" style="width: 600px; margin: 0 auto">
      <el-table-column prop="date" label="日期" width="180"></el-table-column>
      <el-table-column prop="name" label="姓名" width="180"></el-table-column>
      <el-table-column prop="address" label="地址"></el-table-column>
    </el-table>
    <!-- 添加内容 -->
    <el-input class="ipt" v-model="date"></el-input>
    <el-input class="ipt" v-model="name"></el-input>
    <el-input class="ipt" v-model="address"></el-input>
    <br>
    <el-button size="small" type="primary" @click="addTableOptions">表格添加</el-button>
  </div>
</template>

<script>
import { exportExcelByTable } from '@/utils/xlsx';

export default {
  name: 'ExportExcel',
  data() {
    return {
      tableData: [
        {
          date: '2023-12-8',
          name: '挽歌',
          address: '上海市'
        },
      ],
      date: '',
      name: '',
      address: ''
    }
  },
  methods: {
    // 将 table 导出 Excel
    exportExcelByTable() {
      exportExcelByTable(this.$refs.table.$el);
    },
    // 添加表格项
    addTableOptions() {
      const fromdata={
        date:this.date.trim(),
        name:this.name.trim(),
        address:this.address.trim()
      }
      if(fromdata.date || fromdata.name || fromdata.address){
        this.tableData.push(fromdata)
        this.date=""
        this.name=""
        this.address=""
      }
      
    }
  },
};
</script>

<style>
.ipt{
  width: 200px;
  margin: 20px 10px;
}
</style>
