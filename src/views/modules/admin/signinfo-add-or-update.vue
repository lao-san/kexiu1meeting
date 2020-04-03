<template>
  <el-dialog
    :title="!dataForm.id ? '新增' : '修改'"
    :close-on-click-modal="false"
    :visible.sync="visible">
    <el-form :model="dataForm" :rules="dataRule" ref="dataForm" @keyup.enter.native="dataFormSubmit()" label-width="80px">
    <el-form-item label="参会人员id" prop="aId">
      <el-input v-model="dataForm.aId" placeholder="参会人员id"></el-input>
    </el-form-item>
    <el-form-item label="会议id" prop="meetingId">
      <el-input v-model="dataForm.meetingId" placeholder="会议id"></el-input>
    </el-form-item>
    <el-form-item label="姓名" prop="truename">
      <el-input v-model="dataForm.truename" placeholder="姓名"></el-input>
    </el-form-item>
    <el-form-item label="所属机构(单位名称、公司名称" prop="organization">
      <el-input v-model="dataForm.organization" placeholder="所属机构(单位名称、公司名称"></el-input>
    </el-form-item>
    <el-form-item label="职位id" prop="position">
      <el-input v-model="dataForm.position" placeholder="职位id"></el-input>
    </el-form-item>
    <el-form-item label="职称" prop="jobTitle">
      <el-input v-model="dataForm.jobTitle" placeholder="职称"></el-input>
    </el-form-item>
    <el-form-item label="电话" prop="phone">
      <el-input v-model="dataForm.phone" placeholder="电话"></el-input>
    </el-form-item>
    <el-form-item label="参会人员类型id" prop="typeId">
      <el-input v-model="dataForm.typeId" placeholder="参会人员类型id"></el-input>
    </el-form-item>
    <el-form-item label="" prop="typeAttenders">
      <el-input v-model="dataForm.typeAttenders" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="负责人（员工id）" prop="servicer">
      <el-input v-model="dataForm.servicer" placeholder="负责人（员工id）"></el-input>
    </el-form-item>
    <el-form-item label="" prop="servername">
      <el-input v-model="dataForm.servername" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="isPay">
      <el-input v-model="dataForm.isPay" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="签到状态" prop="status">
      <el-input v-model="dataForm.status" placeholder="签到状态"></el-input>
    </el-form-item>
    <el-form-item label="是否完成胸卡打印" prop="badge">
      <el-input v-model="dataForm.badge" placeholder="是否完成胸卡打印"></el-input>
    </el-form-item>
    <el-form-item label="最后签到时间" prop="lastTime">
      <el-input v-model="dataForm.lastTime" placeholder="最后签到时间"></el-input>
    </el-form-item>
    <el-form-item label="备注" prop="note">
      <el-input v-model="dataForm.note" placeholder="备注"></el-input>
    </el-form-item>
    <el-form-item label="注册情况 0, 1, 2, 现场注册" prop="regflag">
      <el-input v-model="dataForm.regflag" placeholder="注册情况 0, 1, 2, 现场注册"></el-input>
    </el-form-item>
    <el-form-item label="创建时间" prop="createTime">
      <el-input v-model="dataForm.createTime" placeholder="创建时间"></el-input>
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
          aId: '',
          meetingId: '',
          truename: '',
          organization: '',
          position: '',
          jobTitle: '',
          phone: '',
          typeId: '',
          typeAttenders: '',
          servicer: '',
          servername: '',
          isPay: '',
          status: '',
          badge: '',
          lastTime: '',
          note: '',
          regflag: '',
          createTime: ''
        },
        dataRule: {
          aId: [
            { required: true, message: '参会人员id不能为空', trigger: 'blur' }
          ],
          meetingId: [
            { required: true, message: '会议id不能为空', trigger: 'blur' }
          ],
          truename: [
            { required: true, message: '姓名不能为空', trigger: 'blur' }
          ],
          organization: [
            { required: true, message: '所属机构(单位名称、公司名称不能为空', trigger: 'blur' }
          ],
          position: [
            { required: true, message: '职位id不能为空', trigger: 'blur' }
          ],
          jobTitle: [
            { required: true, message: '职称不能为空', trigger: 'blur' }
          ],
          phone: [
            { required: true, message: '电话不能为空', trigger: 'blur' }
          ],
          typeId: [
            { required: true, message: '参会人员类型id不能为空', trigger: 'blur' }
          ],
          typeAttenders: [
            { required: true, message: '不能为空', trigger: 'blur' }
          ],
          servicer: [
            { required: true, message: '负责人（员工id）不能为空', trigger: 'blur' }
          ],
          servername: [
            { required: true, message: '不能为空', trigger: 'blur' }
          ],
          isPay: [
            { required: true, message: '不能为空', trigger: 'blur' }
          ],
          status: [
            { required: true, message: '签到状态不能为空', trigger: 'blur' }
          ],
          badge: [
            { required: true, message: '是否完成胸卡打印不能为空', trigger: 'blur' }
          ],
          lastTime: [
            { required: true, message: '最后签到时间不能为空', trigger: 'blur' }
          ],
          note: [
            { required: true, message: '备注不能为空', trigger: 'blur' }
          ],
          regflag: [
            { required: true, message: '注册情况 0, 1, 2, 现场注册不能为空', trigger: 'blur' }
          ],
          createTime: [
            { required: true, message: '创建时间不能为空', trigger: 'blur' }
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
              url: this.$http.adornUrl(`/admin/signinfo/info/${this.dataForm.id}`),
              method: 'get',
              params: this.$http.adornParams()
            }).then(({data}) => {
              if (data && data.code === 0) {
                this.dataForm.aId = data.signInfo.aId
                this.dataForm.meetingId = data.signInfo.meetingId
                this.dataForm.truename = data.signInfo.truename
                this.dataForm.organization = data.signInfo.organization
                this.dataForm.position = data.signInfo.position
                this.dataForm.jobTitle = data.signInfo.jobTitle
                this.dataForm.phone = data.signInfo.phone
                this.dataForm.typeId = data.signInfo.typeId
                this.dataForm.typeAttenders = data.signInfo.typeAttenders
                this.dataForm.servicer = data.signInfo.servicer
                this.dataForm.servername = data.signInfo.servername
                this.dataForm.isPay = data.signInfo.isPay
                this.dataForm.status = data.signInfo.status
                this.dataForm.badge = data.signInfo.badge
                this.dataForm.lastTime = data.signInfo.lastTime
                this.dataForm.note = data.signInfo.note
                this.dataForm.regflag = data.signInfo.regflag
                this.dataForm.createTime = data.signInfo.createTime
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
              url: this.$http.adornUrl(`/admin/signinfo/${!this.dataForm.id ? 'save' : 'update'}`),
              method: 'post',
              data: this.$http.adornData({
                'id': this.dataForm.id || undefined,
                'aId': this.dataForm.aId,
                'meetingId': this.dataForm.meetingId,
                'truename': this.dataForm.truename,
                'organization': this.dataForm.organization,
                'position': this.dataForm.position,
                'jobTitle': this.dataForm.jobTitle,
                'phone': this.dataForm.phone,
                'typeId': this.dataForm.typeId,
                'typeAttenders': this.dataForm.typeAttenders,
                'servicer': this.dataForm.servicer,
                'servername': this.dataForm.servername,
                'isPay': this.dataForm.isPay,
                'status': this.dataForm.status,
                'badge': this.dataForm.badge,
                'lastTime': this.dataForm.lastTime,
                'note': this.dataForm.note,
                'regflag': this.dataForm.regflag,
                'createTime': this.dataForm.createTime
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
