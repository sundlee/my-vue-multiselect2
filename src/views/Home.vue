<template>
  <div class="content">
    <h1>vue-multiselect example</h1>
    <MultiSelect
      v-if="loaded"
      :apis="apis"
    />
  </div>
</template>

<script>
  import axios from 'axios';
  import MultiSelect from '@/components/MultiSelect.vue';

  export default {
    components: {
      MultiSelect,
    },
    data() {
      return {
        loaded: false,
        apis: [],
      }
    },
    mounted() {
      this.load();
    },
    methods: {
      load() {
        console.log('load() - 000');
        this.loaded = false;
        axios.get(`https://run.mocky.io/v3/671b609c-b85b-4a37-9fa9-99454ff0247f`)
          .then((response) => {
            this.apis = response.data.apis;
            // console.log(`load() - apis: ${JSON.stringify(this.apis, null, 4)}`);
            this.loaded = true;
          })
          .catch((err) => {
            console.error(err);
          })
      },
    }
  }
</script>

<style lang="scss">
h1 {
  text-align: center;
  margin-bottom: 30px
}
</style>
