<template>
  <el-dialog
    :title="!dataForm.id ? '新增' : '修改'"
    :close-on-click-modal="false"
    :visible.sync="visible">
    <el-form :model="dataForm" :rules="dataRule" ref="dataForm" @keyup.enter.native="dataFormSubmit()" label-width="80px">
    <el-form-item label="会员id" prop="meetingId">
      <el-input v-model="dataForm.meetingId" placeholder="会员id"></el-input>
    </el-form-item>
    <el-form-item label="参会人员id" prop="attendersId">
      <el-input v-model="dataForm.attendersId" placeholder="参会人员id"></el-input>
    </el-form-item>
    <el-form-item label="论文题目" prop="title">
      <el-input v-model="dataForm.title" placeholder="论文题目"></el-input>
    </el-form-item>
    <el-form-item label="摘要" prop="summary">
      <el-input v-model="dataForm.summary" placeholder="摘要"></el-input>
    </el-form-item>
    <el-form-item label="论文存放地址" prop="paperurl">
      <el-input v-model="dataForm.paperurl" placeholder="论文存放地址"></el-input>
    </el-form-item>
    <el-form-item label="创建时间" prop="createTime">
      <el-input v-model="dataForm.createTime" placeholder="创建时间"></el-input>
    </el-form-item>
    <el-form-item label="是否被删除 状态  0：正常   1：删除" prop="isDel">
      <el-input v-model="dataForm.isDel" placeholder="是否被删除 状态  0：正常   1：删除"></el-input>
    </el-form-item>
    </el-form>
    <span slot="footer" class="dialog-footer">
      <el-button @click="visible = false">取消</el-button>
      <el-button type="primary" @click="dataFormSubmit()">确定</el-button>
    </span>
  </el-dialog>
</template>

<script>
  export default {
    data () {
      return {
        visible: false,
        dataForm: {
          id: 0,
          meetingId: '',
          attendersId: '',
          title: '',
          summary: '',
          paperurl: '',
          createTime: '',
          isDel: ''
        },
        dataRule: {
          meetingId: [
            { required: true, message: '会员id不能为空', trigger: 'blur' }
          ],
          attendersId: [
            { required: true, message: '参会人员id不能为空', trigger: 'blur' }
          ],
          title: [
            { required: true, message: '论文题目不能为空', trigger: 'blur' }
          ],
          summary: [
            { required: true, message: '摘要不能为空', trigger: 'blur' }
          ],
          paperurl: [
            { required: true, message: '论文存放地址不能为空', trigger: 'blur' }
          ],
          createTime: [
            { required: true, message: '创建时间不能为空', trigger: 'blur' }
          ],
          isDel: [
            { required: true, message: '是否被删除 状态  0：正常   1：删除不能为空', trigger: 'blur' }
          ]
        }
      }
    },
    methods: {
      init (id) {
        this.dataForm.id = id || 0
        this.visible = true
        this.$nextTick(() => {
          this.$refs['dataForm'].resetFields()
          if (this.dataForm.id) {
            this.$http({
              url: this.$http.adornUrl(`/admin/paper/info/${this.dataForm.id}`),
              method: 'get',
              params: this.$http.adornParams()
            }).then(({data}) => {
              if (data && data.code === 0) {
                this.dataForm.meetingId = data.paper.meetingId
                this.dataForm.attendersId = data.paper.attendersId
                this.dataForm.title = data.paper.title
                this.dataForm.summary = data.paper.summary
                this.dataForm.paperurl = data.paper.paperurl
                this.dataForm.createTime = data.paper.createTime
                this.dataForm.isDel = data.paper.isDel
              }
            })
          }
        })
      },
      // 表单提交
      dataFormSubmit () {
        this.$refs['dataForm'].validate((valid) => {
          if (valid) {
            this.$http({
              url: this.$http.adornUrl(`/admin/paper/${!this.dataForm.id ? 'save' : 'update'}`),
              method: 'post',
              data: this.$http.adornData({
                'id': this.dataForm.id || undefined,
                'meetingId': this.dataForm.meetingId,
                'attendersId': this.dataForm.attendersId,
                'title': this.dataForm.title,
                'summary': this.dataForm.summary,
                'paperurl': this.dataForm.paperurl,
                'createTime': this.dataForm.createTime,
                'isDel': this.dataForm.isDel
              })
            }).then(({data}) => {
              if (data && data.code === 0) {
                this.$message({
                  message: '操作成功',
                  type: 'success',
                  duration: 1500,
                  onClose: () => {
                    this.visible = false
                    this.$emit('refreshDataList')
                  }
                })
              } else {
                this.$message.error(data.msg)
              }
            })
          }
        })
      }
    }
  }
</script>
