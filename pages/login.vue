<template>
  <v-sheet width="500" class="mx-auto">
    <v-form fast-fail @submit.prevent>
      <v-text-field
        v-model="Username"
        label="Username"
        :rules="UsernameRules"
      ></v-text-field>

      <v-text-field
        v-model="Password"
        label="Password"
        :rules="PasswordRules"
      ></v-text-field>

      <v-btn type="submit" block class="mt-2">Submit</v-btn>
    </v-form>
  </v-sheet>
</template>

<script>
export default {
  data: () => ({
    Username: "",
    UsernameRules: [
      (value) => {
        if (value?.length > 0) return true;

        return "Please enter a Username.";
      },
    ],
    PasswordRules: "",
    PasswordRules: [
      (value) => {
        if (value?.length > 0) return true;

        return "Password needs to be at least 8 characters.";
      },
    ],
  }),
};
</script>
