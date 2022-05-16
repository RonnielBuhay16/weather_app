<script>
export default {
  props: {
    name : String,
    country : String,
    curr_date : String
  }
}
</script>

<template>
     <div class="location-box">
          <div class="location">{{ name }}, {{ country }}</div>
          <div class="date">{{ curr_date }}</div>
        </div>
</template>

<style>
.location-box .location {
  color: #FFF;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.location-box .date {
  color: #FFF;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}
</style>