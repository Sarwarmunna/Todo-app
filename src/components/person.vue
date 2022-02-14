<template>
  <div class="person">
    <h1>Name:{{ name  }}</h1>
    <h2>Age:{{ age }}</h2>
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Earum mollitia labore, 
      harum nisi deleniti aperiam distinctio quis! Eligendi quam ullam deleniti,
       ex omnis cupiditate ad minima tempore, doloribus fugit nam.</p> 
       <slot/>

  </div>
</template>
<script>
export default {
  props:["name","age"],
}
</script>
<style>
.person{
  background: red;
  display: block;
}
</style>