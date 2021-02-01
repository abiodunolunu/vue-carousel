<template>
  <div class="slide" :style="{ backgroundImage: `url(${image})` }">
   <a href="#">{{text}}</a>
  </div>
</template>

<script>
export default {
  props: ["image", "text"],
};
</script>

<style>
.slide {
  height: 100%;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;

  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;
}

.slide a {
  text-decoration: none;
  background: #ffaa00;
  font-size: 20px;
  color: #eee;
  width: fit-content;
  padding: 10px 20px;
  margin: auto;
  border-radius: 5px;
}
</style>