<template>
  <v-dialog width="600" :fullscreen="$vuetify.breakpoint.smAndDown" v-model="dialog" lazy>
    <v-btn class="success" flat slot="activator">Add new project</v-btn>
    <v-card>
      <v-toolbar color="success" card flat>
        <v-btn icon @click="dialog = false">
          <v-icon color="white">arrow_back</v-icon>
        </v-btn>
        <v-card-title class="title font-weight-regular white--text">Add new project</v-card-title>
        <v-spacer></v-spacer>
      </v-toolbar>
      <v-card-text>
        <v-form class="px-3" ref="form">
          <v-text-field label="Title" prepend-icon="folder" v-model="title" :rules="inputRules"></v-text-field>
          <v-textarea label="Information" prepend-icon="edit" v-model="content"></v-textarea>
          <v-btn
            depressed
            :large="$vuetify.breakpoint.smAndDown"
            :block="$vuetify.breakpoint.smAndDown"
            color="primary"
            @click="submit"
          >Add</v-btn>
        </v-form>
      </v-card-text>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      content: "",
      dialog: false,
      inputRules: [v => v && v.length >= 3 || "Minimum characters is 3"]
    };
  },
  methods: {
    submit() {
      if (this.$refs.form.validate()) {
        this.dialog = false
        this.$emit('created-new-project')
      }
    }
  },
  watch: {
    dialog() {
      if (this.$refs.form) {
        this.$refs.form.reset();
      }
    }
  }
};
</script>

