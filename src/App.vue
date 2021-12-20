<template>
  <div class="container">
    <GlobalHeader :user="currentUser"></GlobalHeader>
    <!-- <column-list :list="list"></column-list> -->
    <ValidateFormVue @form-submit="onFormSubmit">
      <div class="mb3">
        <label for="exampleInputEmail" class="form-label">邮箱地址</label>
        <ValidateInputVue
          :rules="emailRules"
          v-model="emailVal"
          typeof="text"
          placeholder="请输入邮箱地址"
          ref="inputRef"
        ></ValidateInputVue>
        {{ emailVal }}
      </div>
      <div class="mb-3">
        <label for="exampleInputPassword1" class="form-label">密码</label>
        <ValidateInputVue
          type="password"
          placeholder="请输入密码"
          :rules="passwordRules"
          class="form-control"
          id="exampleInputPassword1"
        />
      </div>
      <template #submit>
        <span class="btn btn-danger">Submit</span>
      </template>
    </ValidateFormVue>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from "vue";
import "bootstrap/dist/css/bootstrap.min.css";
import ColumnList, { ColumnProps } from "./components/ColumnList.vue";
import GlobalHeader, { UserProps } from "./components/GlobalHeader.vue";
import ValidateInputVue, { RulesProp } from "./components/ValidateInput.vue";
import ValidateFormVue from "./components/ValidateForm.vue";
// import ValidateInput from "./components/ValidateInput.vue";
const testData: ColumnProps[] = [
  {
    id: 1,
    title: "test1的专栏",
    description: "这是的test1专栏，有一段非常有意思的简介，可以更新一下哦",
    avatar: require("./assets/logo.png"),
  },
  {
    id: 2,
    title: "test2的专栏",
    description: "这是的test2专栏，有一段非常有意思的简介，可以更新一下哦",
    avatar: require("./assets/logo.png"),
  },
  {
    id: 3,
    title: "test3的专栏",
    description: "这是的test3专栏，有一段非常有意思的简介，可以更新一下哦",
    avatar: "",
  },
  {
    id: 4,
    title: "test4的专栏",
    description: "这是的test4专栏，有一段非常有意思的简介，可以更新一下哦",
    avatar: require("./assets/logo.png"),
  },
  {
    id: 5,
    title: "test5的专栏",
    description: "这是的test5专栏，有一段非常有意思的简介，可以更新一下哦",
    avatar: require("./assets/logo.png"),
  },
  {
    id: 6,
    title: "test6的专栏",
    description: "这是的test6专栏，有一段非常有意思的简介，可以更新一下哦",
    avatar: require("./assets/logo.png"),
  },
];
const currentUser: UserProps = {
  isLogin: true,
  name: "Zane",
};
export default defineComponent({
  name: "App",
  components: {
    // ColumnList,
    GlobalHeader,
    ValidateInputVue,
    ValidateFormVue,
  },
  setup() {
    const inputRef = ref<any>();
    const emailVal = ref("");
    const emailRules: RulesProp = [
      { type: "required", message: "电子邮箱不能为空" },
      { type: "email", message: "请输入正确的电子邮箱格式" },
    ];
    const passwordRules: RulesProp = [
      { type: "required", message: "密码不能为空" },
      {
        type: "password",
        message:
          "密码格式不正确，最少6位，包括至少1个大写字母，1个小写字母，1个数字，1个特殊字符",
      },
    ];
    const emailReg =
      /^([a-zA-Z0-9_-])+@([a-zA-Z0-9_-])+((\.[a-zA-Z0-9_-]{2,3}){1,2})$/;
    const emailRef = reactive({
      val: "",
      error: false,
      message: "",
    });
    const validateEmail = () => {
      if (emailRef.val.trim() === "") {
        emailRef.error = true;
        emailRef.message = "can not be empty";
      } else if (!emailReg.test(emailRef.val)) {
        emailRef.error = true;
        emailRef.message = "should be valid email";
      } else {
        emailRef.error = false;
      }
    };
    const onFormSubmit = (result: boolean) => {
      console.log(inputRef.value.validateInput());
      console.log("1234", result);
    };
    return {
      list: testData,
      currentUser,
      emailRef,
      validateEmail,
      emailRules,
      emailVal,
      passwordRules,
      onFormSubmit,
      inputRef,
    };
  },
});
</script>

<style></style>
