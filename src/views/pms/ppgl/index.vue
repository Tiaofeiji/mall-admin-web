<template>
  <div class="app-container">
    <el-card class="filter-container" shadow="never">
      <div>
        <i class="el-icon-search"></i>
        <span>查询条件</span>
        <el-button
          style="float: right"
          @click="searchPpglList()"
          type="primary"
          size="small">
          查询
        </el-button>
      </div>
      <div style="margin-top: 10px">
        <el-form :inline="true" :model="listQuery" class="demo-form-inline">
          <el-form-item label="品牌">
            <el-input v-model="listQuery.keyword" placeholder="品牌关键字"></el-input>
          </el-form-item>
        </el-form>
      </div>
    </el-card>
    <div class="table-container">
      <el-table
        :data="list"
        style="width: 100%">
        <el-table-column
          type="selection"
          width="55">
        </el-table-column>
        <el-table-column
          prop="id"
          label="编号"
          width="180">
        </el-table-column>
        <el-table-column
          prop="name"
          label="名称"
          width="180">
        </el-table-column>
        <el-table-column
          prop="firstLetter"
          label="品牌首字母">
        </el-table-column>
        <el-table-column label="操作" width="200" align="center">
          <template slot-scope="scope">
            <el-button size="mini" @click="handleUpdate(scope.$index, scope.row)">编辑
            </el-button>
            <el-button size="mini" type="danger">删除
            </el-button>
          </template>
        </el-table-column>
      </el-table>
    </div>
    <div class="pagination-container">
      <el-pagination
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :current-page.sync="listQuery.pageNum"
        :page-sizes="[10, 20, 30, 40]"
        :page-size="listQuery.pageSize"
        layout="total, sizes, prev, pager, next, jumper"
        :total="total">
      </el-pagination>
    </div>
  </div>
</template>

<script>
  import {fetchList, updateShowStatus, updateFactoryStatus, deleteBrand} from '@/api/brand'

  export default {
    name: "ppglList",
    data() {
      return {
        listQuery: {
          keyword: null,
          pageNum: 1,
          pageSize: 10
        },
        list: null,
        total: null,
      }
    },
    created() {
      this.searchPpglList();
    },
    methods: {
      getList() {
        fetchList(this.listQuery).then(response => {
          this.listLoading = false;
          this.list = response.data.list;
          this.total = response.data.total;
          this.totalPage = response.data.totalPage;
          this.pageSize = response.data.pageSize;
        });
      },
      searchPpglList() {
        this.pageNum = 1;
        this.getList();
      },
      handleSizeChange(val) {
        this.listQuery.pageNum = 1;
        this.listQuery.pageSize = val;
        this.getList();
      },
      handleCurrentChange(val) {
        this.listQuery.pageNum = val;
        this.getList();
      },
      handleUpdate:function(index, row){
        this.$router.push({path: '/pms/updatePpgl', query: {id: row.id}})
      }
    }
  }
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
</style>
