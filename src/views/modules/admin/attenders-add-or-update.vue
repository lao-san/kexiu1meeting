<template>
  <el-dialog
    :title="!dataForm.id ? '新增' : '修改'"
    :close-on-click-modal="false"
    :visible.sync="visible">
    <el-form :model="dataForm" :rules="dataRule" ref="dataForm" @keyup.enter.native="dataFormSubmit()" label-width="80px">
    <el-form-item label="会议id" prop="meetingId">
      <el-input v-model="dataForm.meetingId" placeholder="会议id"></el-input>
    </el-form-item>
    <el-form-item label="会员id" prop="memberId">
      <el-input v-model="dataForm.memberId" placeholder="会员id"></el-input>
    </el-form-item>
    <el-form-item label="姓名" prop="name">
      <el-input v-model="dataForm.name" placeholder="姓名"></el-input>
    </el-form-item>
    <el-form-item label="所属机构(单位名称、公司名称)" prop="organization">
      <el-input v-model="dataForm.organization" placeholder="所属机构(单位名称、公司名称)"></el-input>
    </el-form-item>
    <el-form-item label="职位" prop="positionId">
      <el-input v-model="dataForm.positionId" placeholder="职位"></el-input>
    </el-form-item>
    <el-form-item label="职称" prop="jobTitle">
      <el-input v-model="dataForm.jobTitle" placeholder="职称"></el-input>
    </el-form-item>
    <el-form-item label="电话" prop="phone">
      <el-input v-model="dataForm.phone" placeholder="电话"></el-input>
    </el-form-item>
    <el-form-item label="邮箱" prop="email">
      <el-input v-model="dataForm.email" placeholder="邮箱"></el-input>
    </el-form-item>
    <el-form-item label="办公电话" prop="officephone">
      <el-input v-model="dataForm.officephone" placeholder="办公电话"></el-input>
    </el-form-item>
    <el-form-item label="参会人员类型id" prop="typeId">
      <el-input v-model="dataForm.typeId" placeholder="参会人员类型id"></el-input>
    </el-form-item>
    <el-form-item label="参会意向" prop="intention">
      <el-input v-model="dataForm.intention" placeholder="参会意向"></el-input>
    </el-form-item>
    <el-form-item label="住宿要求" prop="room">
      <el-input v-model="dataForm.room" placeholder="住宿要求"></el-input>
    </el-form-item>
    <el-form-item label="接送要求" prop="transfer">
      <el-input v-model="dataForm.transfer" placeholder="接送要求"></el-input>
    </el-form-item>
    <el-form-item label="负责人（员工id）" prop="servicer">
      <el-input v-model="dataForm.servicer" placeholder="负责人（员工id）"></el-input>
    </el-form-item>
    <el-form-item label="备注" prop="note">
      <el-input v-model="dataForm.note" placeholder="备注"></el-input>
    </el-form-item>
    <el-form-item label="联系电话" prop="account">
      <el-input v-model="dataForm.account" placeholder="联系电话"></el-input>
    </el-form-item>
    <el-form-item label="联系邮箱" prop="emailLx">
      <el-input v-model="dataForm.emailLx" placeholder="联系邮箱"></el-input>
    </el-form-item>
    <el-form-item label="注册情况 0, 1, 2, 现场注册" prop="regflag">
      <el-input v-model="dataForm.regflag" placeholder="注册情况 0, 1, 2, 现场注册"></el-input>
    </el-form-item>
    <el-form-item label="创建时间" prop="createTime">
      <el-input v-model="dataForm.createTime" placeholder="创建时间"></el-input>
    </el-form-item>
    <el-form-item label="修改时间" prop="modifyTime">
      <el-input v-model="dataForm.modifyTime" placeholder="修改时间"></el-input>
    </el-form-item>
    <el-form-item label="创建者" prop="creater">
      <el-input v-model="dataForm.creater" placeholder="创建者"></el-input>
    </el-form-item>
    <el-form-item label="修改者" prop="modifier">
      <el-input v-model="dataForm.modifier" placeholder="修改者"></el-input>
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
          memberId: '',
          name: '',
          organization: '',
          positionId: '',
          jobTitle: '',
          phone: '',
          email: '',
          officephone: '',
          typeId: '',
          intention: '',
          room: '',
          transfer: '',
          servicer: '',
          note: '',
          account: '',
          emailLx: '',
          regflag: '',
          createTime: '',
          modifyTime: '',
          creater: '',
          modifier: '',
          isDel: ''
        },
        dataRule: {
          meetingId: [
            { required: true, message: '会议id不能为空', trigger: 'blur' }
          ],
          memberId: [
            { required: true, message: '会员id不能为空', trigger: 'blur' }
          ],
          name: [
            { required: true, message: '姓名不能为空', trigger: 'blur' }
          ],
          organization: [
            { required: true, message: '所属机构(单位名称、公司名称)不能为空', trigger: 'blur' }
          ],
          positionId: [
            { required: true, message: '职位不能为空', trigger: 'blur' }
          ],
          jobTitle: [
            { required: true, message: '职称不能为空', trigger: 'blur' }
          ],
          phone: [
            { required: true, message: '电话不能为空', trigger: 'blur' }
          ],
          email: [
            { required: true, message: '邮箱不能为空', trigger: 'blur' }
          ],
          officephone: [
            { required: true, message: '办公电话不能为空', trigger: 'blur' }
          ],
          typeId: [
            { required: true, message: '参会人员类型id不能为空', trigger: 'blur' }
          ],
          intention: [
            { required: true, message: '参会意向不能为空', trigger: 'blur' }
          ],
          room: [
            { required: true, message: '住宿要求不能为空', trigger: 'blur' }
          ],
          transfer: [
            { required: true, message: '接送要求不能为空', trigger: 'blur' }
          ],
          servicer: [
            { required: true, message: '负责人（员工id）不能为空', trigger: 'blur' }
          ],
          note: [
            { required: true, message: '备注不能为空', trigger: 'blur' }
          ],
          account: [
            { required: true, message: '联系电话不能为空', trigger: 'blur' }
          ],
          emailLx: [
            { required: true, message: '联系邮箱不能为空', trigger: 'blur' }
          ],
          regflag: [
            { required: true, message: '注册情况 0, 1, 2, 现场注册不能为空', trigger: 'blur' }
          ],
          createTime: [
            { required: true, message: '创建时间不能为空', trigger: 'blur' }
          ],
          modifyTime: [
            { required: true, message: '修改时间不能为空', trigger: 'blur' }
          ],
          creater: [
            { required: true, message: '创建者不能为空', trigger: 'blur' }
          ],
          modifier: [
            { required: true, message: '修改者不能为空', trigger: 'blur' }
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
              url: this.$http.adornUrl(`/admin/attenders/info/${this.dataForm.id}`),
              method: 'get',
              params: this.$http.adornParams()
            }).then(({data}) => {
              if (data && data.code === 0) {
                this.dataForm.meetingId = data.attenders.meetingId
                this.dataForm.memberId = data.attenders.memberId
                this.dataForm.name = data.attenders.name
                this.dataForm.organization = data.attenders.organization
                this.dataForm.positionId = data.attenders.positionId
                this.dataForm.jobTitle = data.attenders.jobTitle
                this.dataForm.phone = data.attenders.phone
                this.dataForm.email = data.attenders.email
                this.dataForm.officephone = data.attenders.officephone
                this.dataForm.typeId = data.attenders.typeId
                this.dataForm.intention = data.attenders.intention
                this.dataForm.room = data.attenders.room
                this.dataForm.transfer = data.attenders.transfer
                this.dataForm.servicer = data.attenders.servicer
                this.dataForm.note = data.attenders.note
                this.dataForm.account = data.attenders.account
                this.dataForm.emailLx = data.attenders.emailLx
                this.dataForm.regflag = data.attenders.regflag
                this.dataForm.createTime = data.attenders.createTime
                this.dataForm.modifyTime = data.attenders.modifyTime
                this.dataForm.creater = data.attenders.creater
                this.dataForm.modifier = data.attenders.modifier
                this.dataForm.isDel = data.attenders.isDel
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
              url: this.$http.adornUrl(`/admin/attenders/${!this.dataForm.id ? 'save' : 'update'}`),
              method: 'post',
              data: this.$http.adornData({
                'id': this.dataForm.id || undefined,
                'meetingId': this.dataForm.meetingId,
                'memberId': this.dataForm.memberId,
                'name': this.dataForm.name,
                'organization': this.dataForm.organization,
                'positionId': this.dataForm.positionId,
                'jobTitle': this.dataForm.jobTitle,
                'phone': this.dataForm.phone,
                'email': this.dataForm.email,
                'officephone': this.dataForm.officephone,
                'typeId': this.dataForm.typeId,
                'intention': this.dataForm.intention,
                'room': this.dataForm.room,
                'transfer': this.dataForm.transfer,
                'servicer': this.dataForm.servicer,
                'note': this.dataForm.note,
                'account': this.dataForm.account,
                'emailLx': this.dataForm.emailLx,
                'regflag': this.dataForm.regflag,
                'createTime': this.dataForm.createTime,
                'modifyTime': this.dataForm.modifyTime,
                'creater': this.dataForm.creater,
                'modifier': this.dataForm.modifier,
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
