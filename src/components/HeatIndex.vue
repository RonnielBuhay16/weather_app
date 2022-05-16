<script>
export default {
  props: {
    temp : Number,
  }
}
</script>

<template>
     <div class="title-box">
          <div class="title">Heat Index</div>
        </div>
          <div class="temp-box">
          <div class="temp">{{ temp }}°c</div>
        </div>
</template>

<style>
.title-box .title {
  color: #FFF;
  font-size: 32px;
  font-weight: 700;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
 
}
.temp-box {
  text-align: center;
}

.temp-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #FFF;
  font-size: 102px;
  font-weight: 900;

  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color:rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0px;

  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>