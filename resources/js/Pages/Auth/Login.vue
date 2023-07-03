

<script setup>

import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';

defineProps({
    canResetPassword: {
        type: Boolean,
    },
    status: {
        type: String,
    },
});

const form = useForm({
    email: '',
    password: '',
    remember: false,
});

const submit = () => {
    form.post(route('login'), {
        onFinish: () => form.reset('password'),
    });
};
</script>

<template>
    <div class="home">
      <div class="container contenedor">
      <div class="screen">
          <div class="screen__content">

            <form id ="formulario" class="login" @submit.prevent="submit">
       
    
        <h1 class="texto">INICIAR SESION</h1>
        <br>
        <div v-if="status" class="mb-4 font-medium text-sm text-green-600">
            {{ status }}
        </div>
        <div>
                <InputLabel for="email" value="Correo Electronico" />

                <TextInput
                    id="email"
                    type="email"
                    class="mt-1 block w-full"
                    v-model="form.email"
                    required
                    autofocus
                    autocomplete="username"
                />

                <InputError class="mt-2" :message="form.errors.email" />
            </div>

            <div class="mt-4">
                <InputLabel for="password" value="Contraseña" />

                <TextInput
                    id="password"
                    type="password"
                    class="mt-1 block w-full"
                    v-model="form.password"
                    required
                    autocomplete="current-password"
                />

                <InputError class="mt-2" :message="form.errors.password" />
            </div>
                <br>
        <PrimaryButton class="ml-4" :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                   " Iniciar Sesión "
                </PrimaryButton>	
                <br>
                <br>
                <br>
                <br>
                
        <PrimaryButton class="ml-4" :class="{ 'opacity-5': form.processing }" :disabled="form.processing">
            <Link
                    v-if="canResetPassword"
                    :href="route('password.request')"
                    class=""
                >
                    olvidaste tu contraseña?
                </Link>
                </PrimaryButton>	

 
              </form>
        
          </div>
          <div class="screen__background">
              <span class="screen__background__shape screen__background__shape4"></span>
              <span class="screen__background__shape screen__background__shape3"></span>		
              <span class="screen__background__shape screen__background__shape2"></span>
              <span class="screen__background__shape screen__background__shape1"></span>
          </div>		
      </div>
  </div>
    </div>
  </template>
  
 



  <style >
  #formulario{
    text-align: center;width: 100%;padding-top:140px
  }
  #olvido{
    font-size: 15px;font-family: cursive;font-weight: 900;text-align: right;margin-top:10px
  }
  * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;	
      font-family: Raleway, sans-serif;
  }
  
  body {
      background: linear-gradient(90deg, #1cd416, #06cd70);		
  }
  
  .contenedor {
      display: flex;
      align-items: center;
      justify-content: center;
      min-height: 100vh;
  }
  
  .screen {		
      background: linear-gradient(90deg, #290fef, #7C78B8);		
      position: relative;	
      height: 600px;
      width: 360px;	
      box-shadow: 0px 0px 24px #09baeb;
  }
  
  .screen__content {
      z-index: 1;
      position: relative;	
      height: 100%;
  }
  
  .screen__background {		
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      z-index: 0;
      -webkit-clip-path: inset(0 0 0 0);
      clip-path: inset(0 0 0 0);	
  }
  
  .screen__background__shape {
      transform: rotate(45deg);
      position: absolute;
  }
  
  .screen__background__shape1 {
      height: 520px;
      width: 520px;
      background: #FFF;	
      top: -50px;
      right: 120px;	
      border-radius: 0 72px 0 0;
  }
  
  .screen__background__shape2 {
      height: 220px;
      width: 220px;
      background: #1e06d5;	
      top: -172px;
      right: 0;	
      border-radius: 32px;
  }
  
  .screen__background__shape3 {
      height: 540px;
      width: 190px;
      background: linear-gradient(270deg, #4a74f3, #322d9d);
      top: -24px;
      right: 0;	
      border-radius: 32px;
  }
  
  .screen__background__shape4 {
      height: 400px;
      width: 200px;
      background: #5b55db;	
      top: 420px;
      right: 50px;	
      border-radius: 60px;
  }
  
  .login {
      width: 920px;
      padding: 60px;
      padding-top: 226px;
  }
  
  .login__field {
      padding: 20px 0px;	
      position: relative;	
  }
  
  .login__icon {
      position: absolute;
      top: 30px;
      color: #6a66b5;
  }
  
  .login__input {
      border: none;
      border-bottom: 2px solid #D1D1D4;
      background: none;
      padding: 10px;
      padding-left: 24px;
      font-weight: 700;
      width: 75%;
      transition: .2s;
  }
  
  .login__input:active,
  .login__input:focus,
  .login__input:hover {
      outline: none;
      border-bottom-color: #6A679E;
  }
  
  .login__submit {
      background: #fff;
      font-size: 14px;
      margin-top: 30px;
      padding: 16px 20px;
      border-radius: 26px;
      border: 1px solid #D4D3E8;
      text-transform: uppercase;
      font-weight: 700;
      display: flex;
      align-items: center;
      width: 100%;
      color: #1d14ba;
      box-shadow: 0px 2px 2px #2211bd;
      cursor: pointer;
      transition: .2s;
  }
  
  .login__submit:active,
  .login__submit:focus,
  .login__submit:hover {
      border-color: #6A679E;
      outline: none;
  }
  
  .button__icon {
      font-size: 24px;
      margin-left: auto;
      color: #7875B5;
  }
  
  .social-login {	
      position: absolute;
      height: 140px;
      width: 160px;
      text-align: center;
      bottom: 0px;
      right: 0px;
      color: #fff;
  }
  
  .social-icons {
      display: flex;
      align-items: center;
      justify-content: center;
  }
  
  .social-login__icon {
      padding: 20px 10px;
      color: #fff;
      text-decoration: none;	
      text-shadow: 0px 0px 8px #7875B5;
  }
  
  .social-login__icon:hover {
      transform: scale(1.5);	
  }
  #titulo{
    font-family: cursive;
      font-weight: 600;
      margin-bottom: 0px;
      color: #3ab250;
  }
  #cuerpo{
      background:rgb(231, 12, 12)
  }
  .texto{
    color: #191970;
  font-family: Calibri, sans-serif;
  font-weight: bold;
  font-size: 24px;
}
  </style>