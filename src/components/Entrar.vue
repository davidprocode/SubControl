<script setup lang="ts">
import { reactive } from 'vue'
import { Button, Input, Form, Checkbox } from 'ant-design-vue'

interface LoginFormState {
  usuario: string
  senha: string
  remember: boolean
}

const formState = reactive<LoginFormState>({
  usuario: '',
  senha: '',
  remember: false,
})

const rules = {
  usuario: [{ required: true, message: 'Por favor, insira seu nome de usuário!', trigger: 'blur' }],
  senha: [
    { required: true, message: 'Por favor, insira sua senha!', trigger: 'blur' },
    { min: 6, message: 'A senha deve ter pelo menos 6 caracteres', trigger: 'blur' },
  ],
}

function handleSubmit() {
  console.log('Dados de login:', formState)
  // Aqui você pode adicionar a lógica de autenticação
}

function resetForm() {
  formState.usuario = ''
  formState.senha = ''
  formState.remember = false
}
</script>

<template>
  <Form
    :model="formState"
    :rules="rules"
    @finish="handleSubmit"
    layout="vertical"
    class="form-login"
  >
    <Form.Item label="Usuário" name="usuario" has-feedback>
      <Input v-model:value="formState.usuario" placeholder="Digite seu nome de usuário" />
    </Form.Item>

    <Form.Item label="Senha" name="senha" has-feedback>
      <Input.Password v-model:value="formState.senha" placeholder="Digite sua senha" />
    </Form.Item>

    <Form.Item name="remember">
      <Checkbox v-model:checked="formState.remember"> Lembrar de mim </Checkbox>
    </Form.Item>

    <Form.Item>
      <Button type="primary" html-type="submit" block> Entrar </Button>
      <Button html-type="button" @click="resetForm" block style="margin-top: 8px"> Limpar </Button>
    </Form.Item>

    <div class="links">
      <a href="#recuperar-senha">Esqueceu a senha?</a>
      <a href="#cadastro" style="margin-top: 8px">Criar nova conta</a>
    </div>
  </Form>
</template>

<style scoped>
.form-login {
  max-width: 400px;
  margin: 40px auto;
  padding: 24px;
  border: 1px solid #e8e8e8;
  border-radius: 8px;
  background: white;
}

.links {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 16px;
}

.links a {
  color: #1890ff;
  text-decoration: none;
}

.links a:hover {
  text-decoration: underline;
}
</style>
