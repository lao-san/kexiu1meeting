<template>
  <div class="mod-oss">
    <el-form :inline="true" :model="dataForm">
      <el-form-item>
        <el-button type="primary" @click="uploadHandle()">上传文件</el-button>
      </el-form-item>
    </el-form>
    
    <el-table
      :data="dataList"
      border
      v-loading="dataListLoading"
      style="width: 100%;">
      <el-table-column
        prop="fileName"
        header-align="center"
        align="center"
        width="200"
        label="文件(目录)名">
        <template slot-scope="scope">
          <el-button type="text" size="small" @click="activeFileHandle(scope.row.fileName, scope.row.suffix)">{{scope.row.fileName}}</el-button>
        </template>
      </el-table-column>
      <el-table-column
        prop="size"
        header-align="center"
        align="center"
        label="大小">
      </el-table-column>
      <el-table-column
        prop="modifyTime"
        header-align="center"
        align="center"
        width="180"
        label="最后修改时间">
      </el-table-column>
      <el-table-column
        fixed="right"
        header-align="center"
        align="center"
        width="150"
        label="操作">
        <template slot-scope="scope">
          <el-button type="text" size="small" @click="deleteHandle(scope.row.id)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
    <!-- 弹窗, 上传文件 -->
    <upload v-if="uploadVisible" ref="upload" @refreshDataList="getDataList"></upload>
  </div>
</template>

<script>
  import Upload from './upload-img'
  import Filemanager from './filemanager'
  export default {
    data () {
      return {
        activepath: '',
        dataForm: {},
        dataList: [],
        dataListLoading: false,
        uploadVisible: false
      }
    },
    components: {
      Upload,
      Filemanager
    },
    activated () {
      this.getDataList()
    },
    methods: {
      // 获取数据列表
      getDataList () {
        this.dataListLoading = true
        this.$http({
          url: this.$http.adornUrl('/sys/filemanager/list'),
          method: 'get',
          params: this.$http.adornParams({
            'activepath': this.activepath
          })
        }).then(({data}) => {
          if (data && data.code === 0) {
            // console.log(data.resultList)
            this.dataList = data.resultList
            this.activepath = data.activepath
          } else {
            this.dataList = []
          }
          this.dataListLoading = false
        })
      },
      activeFileHandle (fileName, suffix) {
        // console.log(suffix)
        // console.log(fileName)
        this.activepath += '/' + fileName
        if (suffix === '' || suffix === null) {
          this.getDataList()
        }
      },
      // 上传文件
      uploadHandle () {
        this.uploadVisible = true
        this.$nextTick(() => {
          this.$refs.upload.init()
        })
      },
      // 删除
      deleteHandle (id) {
        var ids = id ? [id] : this.dataListSelections.map(item => {
          return item.id
        })
        this.$confirm(`确定对[id=${ids.join(',')}]进行[${id ? '删除' : '批量删除'}]操作?`, '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(() => {
          this.$http({
            url: this.$http.adornUrl('/sys/oss/delete'),
            method: 'post',
            data: this.$http.adornData(ids, false)
          }).then(({data}) => {
            if (data && data.code === 0) {
              this.$message({
                message: '操作成功',
                type: 'success',
                duration: 1500,
                onClose: () => {
                  this.getDataList()
                }
              })
            } else {
              this.$message.error(data.msg)
            }
          })
        }).catch(() => {})
      }
    }
  }
</script>
