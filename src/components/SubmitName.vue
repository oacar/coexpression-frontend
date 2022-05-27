<template>
  <div>
    <b-form @submit="onSubmit" v-if="show">
      <b-form-group
        id="input-group-1"
        label="ORF Name:"
        label-for="input-1"
        description="Enter the name of the ORF you want to search for."
      >
        <b-form-input
          id="input-1"
          v-model="form.orf_name"
          type="text"
          placeholder="YAL001C"
          required
        ></b-form-input>
      </b-form-group>
      <b-button type="submit" variant="primary">Submit</b-button>
      <!-- <b-button type="reset" variant="danger">Reset</b-button> -->
    </b-form>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        form: {
          orf_name: '',
        },
        orf_data : [],
        show: true
      }
    },
    methods: {
      onSubmit(event) {
        event.preventDefault()
        this.$router.push("/orf_name/"+this.form.orf_name);
      },
    }
  }

</script>