<template>
  <section class="skeleton-card">
    <div class="skeleton-image">
      <span></span>
    </div>
    <div class="skeleton-content">
      <div class="skeleton-title"></div>
      <div class="skeleton-category">
        <div class="category"></div>
        <div class="rating"></div>
      </div>

      <div class="skeleton-description"></div>
      <div class="skeleton-price"></div>
      <div class="skeleton-buttons">
        <div class="skeleton-button"></div>
        <div class="skeleton-button"></div>
      </div>
    </div>
  </section>
</template>

<style scoped>
@keyframes loading {
  0% {
    opacity: 0.7;
  }
  50% {
    opacity: 1;
  }
  100% {
    opacity: 0.7;
  }
}

.skeleton-card {
  border-radius: 4px;
  animation: loading 1.5s infinite;
  display: flex;
  width: 100%;
  height: 500px;
  justify-content: space-between;
}

.skeleton-image {
  width: 450px;
  height: 350px;
  overflow: hidden;
  margin: auto;
  background-color: #ddd;
  margin: 45px;
}
.skeleton-image span {
  display: inline-block;
  width: 100%; /* Lebar gambar akan mengisi lebar kontainer */
  height: 100%;
  background-color: #ddd;
}

.skeleton-content {
  padding: 30px !important;
  width: 100%;
  gap: 20px;
  display: flex;
  flex-direction: column;
}

.skeleton-title {
  width: 100%;
  height: 60px;
  background: #ddd;
  border-radius: 4px;
}

.skeleton-category {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  height: 20px;
  border-radius: 4px;
}

.rating,
.category {
  width: 40%;
  height: 20px;
  background: #ddd;
  border-radius: 4px;
  background: #ddd;
}

.skeleton-description {
  width: 100%;
  height: 190px;
  background: #ddd;
  border-radius: 4px;
  border-block: 2px solid rgba(0, 0, 0, 0.1);
  margin-block: 10px;
}

.skeleton-price {
  width: 50%;
  height: 20px;
  background: #ddd;
  border-radius: 4px;
}

.skeleton-buttons {
  width: 100%;
  display: flex;
  justify-content: space-between;
}

.skeleton-button {
  width: 45%;
  height: 40px;
  background: #ddd;
  border-radius: 4px;
}
</style>
