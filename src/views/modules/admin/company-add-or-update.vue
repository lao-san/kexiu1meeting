<template>
  <el-dialog
    :title="!dataForm.id ? '新增' : '修改'"
    :close-on-click-modal="false"
    :visible.sync="visible"
  >
    <el-form
      :model="dataForm"
      :rules="dataRule"
      ref="dataForm"
      @keyup.enter.native="dataFormSubmit()"
      label-width="100px"
    >
      <el-form-item label="账号" prop="username">
        <el-input v-model="dataForm.username" placeholder="账号"></el-input>
      </el-form-item>
      <el-form-item label="密码" prop="password">
        <el-input v-model="dataForm.password" placeholder="密码"></el-input>
      </el-form-item>
      <el-form-item label="单位名称" prop="companyname">
        <el-input v-model="dataForm.companyname" placeholder="单位名称"></el-input>
      </el-form-item>
      <el-form-item label="单位地址" prop="address">
        <el-input v-model="dataForm.address" placeholder="单位地址"></el-input>
      </el-form-item>
      <el-form-item label="单位电话" prop="telephone">
        <el-input v-model="dataForm.telephone" placeholder="单位电话"></el-input>
      </el-form-item>
      <el-form-item label="联系人姓名" prop="contactname">
        <el-input v-model="dataForm.contactname" placeholder="联系人姓名"></el-input>
      </el-form-item>
      <el-form-item label="联系人电话" prop="cellphone">
        <el-input v-model="dataForm.cellphone" placeholder="联系人电话"></el-input>
      </el-form-item>
      <el-form-item label="统一社会信用代码" prop="uscCode">
        <el-input v-model="dataForm.uscCode" placeholder="统一社会信用代码"></el-input>
      </el-form-item>
      <!-- <el-form-item label="证件扫码件(图片)地址" prop="uscPicture">
      <el-input v-model="dataForm.uscPicture" placeholder="证件扫码件(图片)地址"></el-input>
      </el-form-item>-->
      <!-- <el-form-item label="账号等级" prop="level">
        <el-input v-model="dataForm.level" placeholder="账号等级"></el-input>
      </el-form-item> -->
      <!-- <el-form-item label="是否通过审核 0:未通过 1:通过" prop="isCheck">
      <el-input v-model="dataForm.isCheck" placeholder="是否通过审核 0:未通过 1:通过"></el-input>
      </el-form-item>-->
      <!-- <el-form-item label="创建时间" prop="createTime">
      <el-input v-model="dataForm.createTime" placeholder="创建时间"></el-input>
    </el-form-item>
    <el-form-item label="修改时间" prop="modifyTime">
      <el-input v-model="dataForm.modifyTime" placeholder="修改时间"></el-input>
      </el-form-item>-->
      <!-- <el-form-item label="是否被删除 状态  0：正常   1：删除" prop="isDel">
      <el-input v-model="dataForm.isDel" placeholder="是否被删除 状态  0：正常   1：删除"></el-input>
      </el-form-item>-->
    </el-form>
    <span slot="footer" class="dialog-footer">
      <el-button @click="visible = false">取消</el-button>
      <el-button type="primary" @click="dataFormSubmit()">确定</el-button>
    </span>
  </el-dialog>
</template>

<script>
export default {
  data() {
    return {
      visible: false,
      dataForm: {
        id: 0,
        username: "",
        password: "",
        companyname: "",
        address: "",
        telephone: "",
        contactname: "",
        cellphone: "",
        uscCode: "",
        uscPicture: ""
      },
      dataRule: {
        username: [
          { required: true, message: "账号不能为空", trigger: "blur" }
        ],
        password: [
          { required: true, message: "密码不能为空", trigger: "blur" }
        ],
        companyname: [
          { required: true, message: "单位名称不能为空", trigger: "blur" }
        ],
        address: [
          { required: true, message: "单位地址不能为空", trigger: "blur" }
        ],
        telephone: [
          { required: true, message: "单位电话不能为空", trigger: "blur" }
        ],
        contactname: [
          { required: true, message: "联系人姓名不能为空", trigger: "blur" }
        ],
        cellphone: [
          { required: true, message: "联系人电话不能为空", trigger: "blur" }
        ],
        uscCode: [
          {
            required: true,
            message: "统一社会信用代码(Uniform Social Credit Code不能为空",
            trigger: "blur"
          }
        ],
        uscPicture: [
          {
            required: true,
            message: "证件扫码件(图片)地址不能为空",
            trigger: "blur"
          }
        ],
        level: [
          { required: true, message: "账号等级不能为空", trigger: "blur" }
        ],
        isCheck: [
          {
            required: true,
            message: "是否通过审核 0:未通过 1:通过不能为空",
            trigger: "blur"
          }
        ],
        createTime: [
          { required: true, message: "创建时间不能为空", trigger: "blur" }
        ],
        modifyTime: [
          { required: true, message: "修改时间不能为空", trigger: "blur" }
        ],
        isDel: [
          {
            required: true,
            message: "是否被删除 状态  0：正常   1：删除不能为空",
            trigger: "blur"
          }
        ]
      }
    };
  },
  methods: {
    init(id) {
      this.dataForm.id = id || 0;
      this.visible = true;
      this.$nextTick(() => {
        this.$refs["dataForm"].resetFields();
        if (this.dataForm.id) {
          this.$http({
            url: this.$http.adornUrl(`/admin/company/info/${this.dataForm.id}`),
            method: "get",
            params: this.$http.adornParams()
          }).then(({ data }) => {
            if (data && data.code === 0) {
              this.dataForm.username = data.company.username;
              this.dataForm.password = data.company.password;
              this.dataForm.companyname = data.company.companyname;
              this.dataForm.address = data.company.address;
              this.dataForm.telephone = data.company.telephone;
              this.dataForm.contactname = data.company.contactname;
              this.dataForm.cellphone = data.company.cellphone;
              this.dataForm.uscCode = data.company.uscCode;
              this.dataForm.uscPicture = data.company.uscPicture;
              this.dataForm.level = data.company.level;
              this.dataForm.isCheck = data.company.isCheck;
              this.dataForm.createTime = data.company.createTime;
              this.dataForm.modifyTime = data.company.modifyTime;
              this.dataForm.isDel = data.company.isDel;
            }
          });
        }
      });
    },
    // 表单提交
    dataFormSubmit() {
      this.$refs["dataForm"].validate(valid => {
        if (valid) {
          this.$http({
            url: this.$http.adornUrl(
              `/admin/company/${!this.dataForm.id ? "save" : "update"}`
            ),
            method: "post",
            data: this.$http.adornData({
              id: this.dataForm.id || undefined,
              username: this.dataForm.username,
              password: this.dataForm.password,
              companyname: this.dataForm.companyname,
              address: this.dataForm.address,
              telephone: this.dataForm.telephone,
              contactname: this.dataForm.contactname,
              cellphone: this.dataForm.cellphone,
              uscCode: this.dataForm.uscCode,
              uscPicture: this.dataForm.uscPicture,
              level: this.dataForm.level,
              isCheck: this.dataForm.isCheck,
              createTime: this.dataForm.createTime,
              modifyTime: this.dataForm.modifyTime,
              isDel: this.dataForm.isDel
            })
          }).then(({ data }) => {
            if (data && data.code === 0) {
              this.$message({
                message: "操作成功",
                type: "success",
                duration: 1500,
                onClose: () => {
                  this.visible = false;
                  this.$emit("refreshDataList");
                }
              });
            } else {
              this.$message.error(data.msg);
            }
          });
        }
      });
    }
  }
};
</script>
