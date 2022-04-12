<script>
export default {
  data() {
    return {
      people:[]
    }
  },
  mounted() {
    fetch("https://services.odata.org/TripPinRESTierService/(S(j3a2sx1yypgxj1mpzjgmsrgn))/People")
      .then(response => response.json())
      .then(data => this.people = data.value)
      .catch(error => console.log(error.message));
  }
}
</script>

<template>
<!-- shouldn't have to wrap root component but getting eslinting from Vetur plugin -->
<div>
  <h1>People</h1>
  <ul v-if="people.length">
    <li v-for="person in people" :key="person.UserName">
      {{ person.UserName }}
    </li>
  </ul>
  <div v-else>
    Loading...
  </div>
</div>
</template>


