<script setup>
  import { reactive } from 'vue'
  import { useVuelidate } from '@vuelidate/core'
  import { required, email, minLength  } from '@vuelidate/validators'
  import { useRouter } from "vue-router";
  const router = useRouter()

  const state = reactive({
    eMail: '',
    password: ''
  })

  const rules = {
    eMail: { required, email },
    password: {
      required,
      min: minLength(6)
    }
  }

  const v$ = useVuelidate(rules, state)

  const submit = () => {
    v$.value.$validate();
    if(v$.value.$error) {
      console.log(v$.value.eMail.$error)
    }else{
      router.push('game')
    }
  }

</script>

<template>
  <div class="login">
    <v-card elevation="4" light tag="section">
      <v-form fast-fail @submit.prevent="submit">

        <v-text-field
            v-model.trim="state.eMail"
            label="Email"
            required
        >
        </v-text-field>

        <v-text v-if="v$.eMail.$error">
          {{ v$.eMail.$errors[0].$message }}
        </v-text>

        <v-text-field
            v-model.trim="state.password"
            label="Password"
            required
        >

        </v-text-field>
        <v-text v-if="v$.password.$error">{{ v$.password.$errors[0].$message }}</v-text>
        <v-btn type="submit" color="primary" block class="mt-2">Sign in</v-btn>

      </v-form>
    </v-card>
  </div>
</template>

<style>
  .login{
    max-width: 600px;
    margin: 10px auto;
    box-shadow: 0 0 2px #ccc;
  }
</style>
