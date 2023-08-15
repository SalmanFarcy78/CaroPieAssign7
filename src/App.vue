<template>
  <h3 class="ml-0 bg-orange-400 text-white py-2 px-4"> Carousel </h3>
<div class="container"> 
      <div id="carousel" class="carousel">
        <div v-for="(item, index) in items" :key="index" class="carousel-item">
          <img :src="item" alt="Carousel Item" />
        </div>
      </div>

</div>

<br><br><br><br>
    <h3  class="ml-0 bg-blue-500 text-white font-bold py-2 px-4 rounded">Pie Chart </h3>
    <div class="container"> 
        <div id="carousel" class="carousel">
     <canvas ref="chartCanvas"></canvas>
    </div>
</div>
  </template>
  
  <script setup>
  import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue';
  import Chart from 'Chart.js/dist/Chart.js';
  
  const items = ref([
    'https://images.unsplash.com/photo-1670779462181-052586baae1a?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=870&q=80',
    'https://images.unsplash.com/photo-1670271331172-3d2b4408a801?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=774&q=80',
    'https://images.unsplash.com/photo-1670271331288-0dadad33d11f?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=774&q=80',
    'https://images.unsplash.com/photo-1670271428400-722914171c92?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=870&q=80',
    'https://images.unsplash.com/photo-1623514921350-a7199a6ab657?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=843&q=80',
    'https://images.unsplash.com/photo-1670270631303-89af30135d6d?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=870&q=80',
  ]);
  
  let carousel = null;
 
  onMounted(() => {
    carousel = new Flickity('#carousel', { imagesLoaded: true, });
  });
  onBeforeUnmount(() => {
  Carousel.destroy()
})
  
  // ============== PIE
  
  const chartCanvas = ref(null);
  let chartInstance = null;
  
  const fetchData = () => {
      const data = {
      labels: ['Category A', 'Category B', 'Category C'],
      datasets: [
        {
          data: [30, 40, 20],
          backgroundColor: ['#FF6384', '#36A2EB', '#FFCE56'],
        },
      ],
    };
    return data;
  };
  
  onMounted(() => {
    const chartData = fetchData();
  
    const ctx = chartCanvas.value.getContext('2d');
    chartInstance = new Chart(ctx, {
      type: 'pie',
      data: chartData,
      options: {
        responsive: true,
        maintainAspectRatio: false,
      },
    });
  });
  

  </script>

<style scoped>
.carousel {
  width: 500px;
  height: 300px;
}


.container {
  display: flex;
  flex-direction: column;
  align-items: center; /* Center horizontally */
  justify-content: center; /* Center vertically */
  height: 45vh; /* Set the container height to fill the viewport */
}

</style>
