<template>
  <div>
    <b-row class="mt-5">
      <b-col
        md="8"
        offset-md="2"
        lg="6"
        offset-lg="3"
      >
        <b-card title="登录">
          <b-form>

            <b-form-group label="手机号:">
              <b-form-input
                v-model="$v.user.telephone.$model"
                type="number"
                placeholder="输入您的手机号 "
                :state="validateState('telephone')"
              ></b-form-input>
              <b-form-invalid-feedback :state="validateState('telephone')">
                手机号不符合要求
              </b-form-invalid-feedback>
            </b-form-group>
            <b-form-group label="密码:">
              <b-form-input
                v-model="$v.user.password.$model"
                type="password"
                placeholder="输入您的密码 "
                :state="validateState('password')"
              ></b-form-input>
              <b-form-invalid-feedback :state="validateState('password')">
                密码必须大于等于 6 位
              </b-form-invalid-feedback>
            </b-form-group>
            <b-form-group>
              <b-button
                @click="login"
                variant="primary"
                block
              >登录</b-button>
            </b-form-group>
          </b-form>
        </b-card>
      </b-col>
    </b-row>
  </div>
</template>

<script>
import { required, minLength } from 'vuelidate/lib/validators';
import consumValidator from '../../helper/validator';

export default {
  data() {
    return {
      user: {
        telephone: '',
        password: '',
      },
    };
  },
  validations: {
    user: {
      telephone: {
        required,
        telephone: consumValidator.telephoneValidator,
      },
      password: {
        required,
        minLength: minLength(6),
      },
    },
  },
  methods: {
    // 这里是es6 解构赋值
    validateState(name) {
      const { $dirty, $error } = this.$v.user[name];
      return $dirty ? !$error : null;
    },
    login() {
      console.log('注册成功');
    },
  },
};

</script>
<style scoped>
</style>
