<template>
  <div class="vid-grid">
    <iframe width="100%" height="100%" src="https://www.youtube.com/embed/tgbNymZ7vqY"></iframe>
    <div class="images">
      <img src="https://picsum.photos/150/100" alt />
      <img src="https://picsum.photos/150/100" alt />
      <img src="https://picsum.photos/150/100" alt />
      <img src="https://picsum.photos/150/100" alt />
    </div>
  </div>
</template>

<style scoped>
.vid-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
}
.images {
  display: grid;
  border: 1px solid black;
  grid-template-columns: repeat(2, 1fr);
}
.images img {
  width: 100%;
  object-fit: cover;
}
</style>