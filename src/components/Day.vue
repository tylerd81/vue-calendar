<template>
  <div> 
    <div v-if="date != 0">
      <span class="date">{{date}}</span>
    </div>
    <div class="no-day" v-else>
    </div>
  </div>
</template>

<script>
export default {
  props:['date'],
}
</script>

<style>
span.date {
  padding: .25rem;
  display: inline-block;
  font-weight: bold;
}
</style>