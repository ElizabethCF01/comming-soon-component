<script setup lang="ts">
import { ref } from "vue";

const EMAIL_REQUIRED = "Please fill out this field";
const EMAIL_INVALID = "Please provide a valid email";
const rx: RegExp = /^\w+([.-_+]?\w+)*@\w+([.-]?\w+)*(\.\w{2,10})+$/;
const message = ref("");
const showMessage= ref(false)
const email = ref("");

const checkEmail = (): boolean => {
  if (email.value =="") {
    message.value = EMAIL_REQUIRED;
    showMessage.value=true
    return false;
  }
  if (rx.test(email.value)){
     message.value = ''
     showMessage.value=false
     return true;
    }
  else {
    message.value = EMAIL_INVALID;
    showMessage.value=true
}
  return false;
};
</script>

<template>
  <div class="card d-flex">
    <div class="col-1">
        <div class="header">
      <img class="logo" src="../assets/logo.svg" alt="logo" />
    </div>
    <div class="card-img"></div>
    <div class="card-title">
      <h1 class="title">
        <p class="text-red title-red">We're</p>
        coming soon
      </h1>
    </div>
    <div class="card-text text-red">
      <p>
        Hello fellow shoppers! We're currently building our new fashion store. Add your
        email below to stay up-to-date with announcements and our launch deals.
      </p>
    </div>
    <div class="card-actions d-flex">
      <form class="card-form d-flex" @submit.prevent="checkEmail">
        <div class="form-control d-flex">
            <input
                type="text"
                v-model="email"
                placeholder="Email Address"
                class="rounded"
                :class="{danger: showMessage}"
            />
            <img v-show="showMessage" class="err" src="../assets/icon-error.svg" alt="err"/>
            <button class="btn-submit rounded d-flex" type="submit"><img src="../assets/icon-arrow.svg" alt=">" /></button>
        </div>
        <p class="text-danger">{{ message }}</p>
      </form>
    </div>
    </div>
    <div class="card-img-desktop col-2"></div>
  </div>
</template>

<style scoped>
.text-red {
  color: hsl(0, 36%, 70%);
}
.text-danger{
    color: hsl(0, 93%, 68%);
}
</style>
