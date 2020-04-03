<template>
  <el-dialog
    :title="!dataForm.id ? '新增' : '修改'"
    :close-on-click-modal="false"
    :visible.sync="visible">
    <el-form :model="dataForm" :rules="dataRule" ref="dataForm" @keyup.enter.native="dataFormSubmit()" label-width="80px">
    <el-form-item label="会议id" prop="meetingId">
      <el-input v-model="dataForm.meetingId" placeholder="会议id"></el-input>
    </el-form-item>
    <el-form-item label="账号名称" prop="name">
      <el-input v-model="dataForm.name" placeholder="账号名称"></el-input>
    </el-form-item>
    <el-form-item label="开户银行" prop="bank">
      <el-input v-model="dataForm.bank" placeholder="开户银行"></el-input>
    </el-form-item>
    <el-form-item label="账号" prop="account">
      <el-input v-model="dataForm.account" placeholder="账号"></el-input>
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
          name: '',
          bank: '',
          account: '',
          createTime: '',
          isDel: ''
        },
        dataRule: {
          meetingId: [
            { required: true, message: '会议id不能为空', trigger: 'blur' }
          ],
          name: [
            { required: true, message: '账号名称不能为空', trigger: 'blur' }
          ],
          bank: [
            { required: true, message: '开户银行不能为空', trigger: 'blur' }
          ],
          account: [
            { required: true, message: '账号不能为空', trigger: 'blur' }
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
              url: this.$http.adornUrl(`/admin/moneyaccount/info/${this.dataForm.id}`),
              method: 'get',
              params: this.$http.adornParams()
            }).then(({data}) => {
              if (data && data.code === 0) {
                this.dataForm.meetingId = data.moneyAccount.meetingId
                this.dataForm.name = data.moneyAccount.name
                this.dataForm.bank = data.moneyAccount.bank
                this.dataForm.account = data.moneyAccount.account
                this.dataForm.createTime = data.moneyAccount.createTime
                this.dataForm.isDel = data.moneyAccount.isDel
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
              url: this.$http.adornUrl(`/admin/moneyaccount/${!this.dataForm.id ? 'save' : 'update'}`),
              method: 'post',
              data: this.$http.adornData({
                'id': this.dataForm.id || undefined,
                'meetingId': this.dataForm.meetingId,
                'name': this.dataForm.name,
                'bank': this.dataForm.bank,
                'account': this.dataForm.account,
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
