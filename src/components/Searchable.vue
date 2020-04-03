<template>
  <div class="container">
     <h3>Search something below</h3>
     <autocomplete v-on:selected="handleSelected"
        :source="tags"
        :resultsFormatter='formatResults'
        input-class="autocomplete-input"
    >
    </autocomplete>
  </div>
</template>

<script>
import Autocomplete from 'vuejs-auto-complete';
export default {
  name: 'Searchable',
  components: {
      Autocomplete
  },
  data() { 
      return {
        tags: []
    }
  },
  async mounted() {
      const res = await fetch('https://expr-integ-ds-005-tag.dev.trservices.io/tags/allTagsAllLocalizations');
      const json = await res.json();
      this.tags = Object.values(json.tags).map(v => ({id: v.tagId, name: v.englishName}));
  },
  methods: {
    handleSelected: (selected) => {
        alert(JSON.stringify(selected));    
    },
    formatResults: (res) => {
        console.warn(res);
    }
  }
}
</script>

<style scoped>
    .container {
        padding: 2em;
        width: 50%;
        border: 1px solid black;
    }
</style>
<style>
    .autocomplete-input {
        min-width: 200px;    
    }
</style>
