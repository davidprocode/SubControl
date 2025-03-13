<script setup lang="ts">
import { reactive } from 'vue'
import { Button, Input, Form, Select, DatePicker } from 'ant-design-vue'
import type { Dayjs } from 'dayjs'

interface FormState {
  usuario: string
  senha: string
  nome: string
  funcao: 'administrador' | 'usuario'
  dataNascimento: Dayjs | null
}

const formState = reactive<FormState>({
  usuario: '',
  senha: '',
  nome: '',
  funcao: 'usuario',
  dataNascimento: null,
})

const rules = {
  usuario: [
    { required: true, message: 'Por favor, insira o nome de usuário', trigger: 'blur' },
    { min: 4, message: 'Mínimo de 4 caracteres', trigger: 'blur' },
  ],
  senha: [
    { required: true, message: 'Por favor, insira a senha', trigger: 'blur' },
    { min: 6, message: 'A senha deve ter pelo menos 6 caracteres', trigger: 'blur' },
  ],
  nome: [{ required: true, message: 'Por favor, insira seu nome completo', trigger: 'blur' }],
  funcao: [{ required: true, message: 'Por favor, selecione a função', trigger: 'change' }],
  dataNascimento: [
    { required: true, message: 'Por favor, selecione a data de nascimento', trigger: 'change' },
  ],
}

function onSubmit() {
  console.log('Dados do formulário:', {
    ...formState,
    dataNascimento: formState.dataNascimento?.format('DD-MM-YYYY'),
  })
}

function resetFields() {
  formState.usuario = ''
  formState.senha = ''
  formState.nome = ''
  formState.funcao = 'usuario'
  formState.dataNascimento = null
}
</script>

<template>
  <Form
    :model="formState"
    :rules="rules"
    @finish="onSubmit"
    layout="vertical"
    class="form-cadastro"
  >
    <Form.Item label="Nome Completo" name="nome" has-feedback>
      <Input v-model:value="formState.nome" placeholder="Digite seu nome completo" />
    </Form.Item>

    <Form.Item label="Nome de Usuário" name="usuario" has-feedback>
      <Input v-model:value="formState.usuario" placeholder="Digite um nome de usuário" />
    </Form.Item>

    <Form.Item label="Senha" name="senha" has-feedback>
      <Input.Password v-model:value="formState.senha" placeholder="Crie uma senha segura" />
    </Form.Item>

    <Form.Item label="Função" name="funcao" has-feedback>
      <Select v-model:value="formState.funcao" placeholder="Selecione a função">
        <Select.Option value="administrador">Administrador</Select.Option>
        <Select.Option value="usuario">Usuário Comum</Select.Option>
      </Select>
    </Form.Item>

    <Form.Item label="Data de Nascimento" name="dataNascimento" has-feedback>
      <DatePicker
        v-model:value="formState.dataNascimento"
        format="DD/MM/YYYY"
        placeholder="Selecione a data"
        style="width: 100%"
      />
    </Form.Item>

    <Form.Item>
      <Button type="primary" html-type="submit" block>Cadastrar</Button>
      <Button html-type="button" @click="resetFields" block style="margin-top: 8px">
        Limpar Campos
      </Button>
    </Form.Item>
  </Form>
</template>

<style scoped>
.form-cadastro {
  max-width: 500px;
  margin: 20px auto;
  padding: 20px;
  border: 1px solid #e8e8e8;
  border-radius: 8px;
}
</style>
