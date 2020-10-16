<template>
  <div class="container">
    <multiselect
      v-model="value"
      :options="options"
      :multiple="true"
      :custom-label="customLabel"
      :close-on-select="false"
      :clear-on-select="false"
      :preserve-search="true"
      :max-height="300"
      placeholder="🔍 메소드 또는 URI 입력"
      select-label="클릭해서 선택"
      deselect-label="클릭해서 선택해제"
      selected-label="선택됨"
      label="apiId"
      track-by="apiId"
      :preselect-first="true"
    >
      <template slot="selection" slot-scope="{ values, search, isOpen }">
        <span class="multiselect__single" v-if="values.length && !isOpen">
          API 리소스 선택 ({{ values.length }})
        </span>
      </template>
      <template slot="option" slot-scope="props">
        <div class="option-label">
          <span class="option-method">
            {{ props.option.method }}
          </span>
          <span class="option-uri">
            {{ props.option.uri }}
          </span>
        </div>
      </template>
      <template slot="placeholder">
        <div class="option-label">
          API 리소스 선택
        </div>
      </template>
    </multiselect>
    <pre class="language-json"><code>{{ value }}</code></pre>
  </div>
</template>

<script>
import Multiselect from 'vue-multiselect';

export default {
  name: 'multipleSelect',
  components: { Multiselect },
  props: {
    apis: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      value: [],
      options: [],
    };
  },
  mounted() {
    console.log(`mounted - apis: ${JSON.stringify(this.apis, null, 4)}`);
    this.options = this.apis;
    // this.value = this.options[0];
  },
  methods: {
    customLabel ({ method, uri }) {
      return `${method} ${uri}`;
    },
  },
}
</script>

<style src="vue-multiselect/dist/vue-multiselect.min.css"></style>
<style>
.container {
  width: 600px;
  margin: auto auto;
}
.container pre {
  padding: 10px;
  text-align: left;
  background-color: #e9e9e9;
}
.option-label {
  font-size: 14px;
  font-weight: normal;
}
.option-method {
  color: purple;
}
.option-uri {

}
</style>
