<script>
export default {
  data() {
    return {
      people:[],
      errorMessage: ''
    }
  },

  async mounted() {
    const uri = "https://services.odata.org/TripPinRESTierService/(S(j3a2sx1yypgxj1mpzjgmsrgn))/People"
    this.errorMessage = '';
    try {        
        const response = await fetch(uri);
        const json = await response.json();
        this.people = json.value;
    } catch (error) {
        this.errorMessage = error.message;
    }
  }
}
</script>

<template>
<!-- shouldn't have to wrap root component but getting eslinting from Vetur plugin -->
<div>
  <h1>People</h1>
  <div v-if="errorMessage">
      Could not retrieve people.
  </div>
  <ul v-else-if="people.length">
    <li v-for="person in people" :key="person.UserName">
      {{ person.UserName }}
    </li>
  </ul>
  <div v-else>
    Loading...
  </div>
</div>
</template>


