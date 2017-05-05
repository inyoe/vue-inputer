# vue-inputer

# demo
http://demo.rabifoo.com/#/inputer

### Usage

html:
````html
<div class="item">
  <label>Name</label>
  <inputer v-model="formData.name"
           ruleType="*"
           tipNull="用户名不能为空"
           tipError="任意不为空即可"
           maxlength="20"
           placeholder="用户名"
           ref="name"></inputer>
</div>

<div class="item">
  <label>Tel</label>
  <inputer v-model="formData.phoneNo"
           ruleType="tel"
           tipNull="手机号码不能为空"
           tipError="请输入正确的手机号码"
           maxlength="11"
           placeholder="手机号"
           ref="phoneNo"></inputer>
</div>

<div class="item">
  <label>Email</label>
  <inputer v-model="formData.email"
           ruleType="email"
           tipNull="邮箱不能为空"
           tipError="请输入正确的邮箱"
           maxlength="20"
           placeholder="用户名"
           ref="email"></inputer>
</div>

<div class="btn-submit" @click="formSubmit">提 交</div>
````

js:
````javascript
formData: {
  name: {
    val: '',
    valid: false
  },
  phoneNo: {
    val: '',
    valid: false
  },
  email: {
    val: '',
    valid: false
  }
}

formSubmit() {
  let data = {};
  for (var key in this.formData) {
    if (this.formData[key].valid) {
      data[key] = this.formData[key].val;
    } else {
      this.$refs[key].onBlur();
    return false;
    }
  }
  console.log(data);
}
````
