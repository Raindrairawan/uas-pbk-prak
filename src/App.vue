<template>
  <div id="app">
    <nav class="navbar">
      <span class="navbar-brand">Weather App</span>
    </nav>
    <div class="task-list">
      <ul>
        <li v-for="task in tasks" :key="task.name">
          <a :href="task.url">{{ task.name }}</a>
        </li>
      </ul>
    </div>
    <div class="container">
      <h1>WEATHER</h1>
      <div class="weather-card">
        <h2>Cuaca</h2>
        <div class="input-group">
          <input type="text" v-model="location" placeholder="Masukkan Lokasi" />
          <button @click="getWeather">Cari</button>
        </div>
        <div v-if="isLoading" class="loading">
          Loading data...
        </div>
        <div v-if="error" class="error">
          {{ error }}
        </div>
        <div v-if="weatherData" class="weather-info">
          <p>Lokasi: {{ weatherData.name }}</p>
          <p>Suhu: {{ weatherData.main.temp }}°C</p>
          <p>Kondisi: {{ weatherData.weather[0].description }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      location: '',
      weatherData: null,
      isLoading: false,
      error: null,
      tasks: [
        { name: 'Tugas 1', url: 'https://raindra-project-cv.netlify.app/?authuser=0&hl=id' },
        { name: 'Tugas 2', url: 'http://223510156-raindra-irawan-tugas1-1nn74xh14.vercel.app/?authuser=0&hl=id' },
        { name: 'Tugas 3', url: 'http://223510156-raindra-irawan-tugas3-8lomcs1pr.vercel.app/?authuser=0&hl=id' },
        { name: 'Tugas 4', url: 'https://223510156-raindra-irawan-tugas4.vercel.app/?authuser=0&hl=id' },
        // Tambahkan lebih banyak tugas sesuai kebutuhan
      ]
    };
  },
  methods: {
    getWeather() {
      this.isLoading = true;
      this.error = null;
      this.weatherData = null;

      const apikey = 'YOUR_API_KEY'; // Replace with your actual API key
      const apiUrl = `https://api.openweathermap.org/data/2.5/weather?q=${this.location}&appid=${apikey}&units=metric`;

      axios
        .get(apiUrl)
        .then((response) => {
          this.weatherData = response.data;
        })
        .catch((error) => {
          this.error = error.message;
        })
        .finally(() => {
          this.isLoading = false;
        });
    },
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  height: 100vh; /* Menggunakan seluruh tinggi layar */
  display: flex;
  justify-content: center;
  align-items: center; /* Pusatkan konten secara vertikal */
  background: linear-gradient(to right, #6dd5ed, #2193b0); /* Gradient background */
}

.container {
  width: 300px; /* Lebar tetap untuk kartu */
  background-color: #fff;
  padding: 20px;
  border-radius: 10px; /* Border radius yang lebih besar */
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* Bayangan yang lebih lembut */
}

.input-group {
  display: flex;
  justify-content: space-between; /* Mengatur jarak antar elemen */
  margin-bottom: 20px;
}

input {
  flex-grow: 1; /* Input mengambil ruang yang tersisa */
  margin-right: 10px; /* Jarak antara input dan tombol */
}

button {
  cursor: pointer;
  background-color: #007bff;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 5px;
  transition: background-color 0.3s ease; /* Animasi transisi untuk background */
}

button:hover {
  background-color: #0056b3; /* Warna berubah ketika di-hover */
}

.loading, .error {
  text-align: center;
  margin-top: 20px;
}

.error {
  color: red;
}

.weather-info {
  text-align: left; /* Teks info cuaca rata kiri */
}

.navbar {
  width: 100%;
  background-color: #007bff; /* Warna latar belakang biru */
  color: white;
  padding: 10px 20px; /* Padding untuk navbar */
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); /* Bayangan untuk navbar */
}

.navbar-brand {
  font-size: 20px; /* Ukuran font untuk brand */
}

.task-list ul {
  list-style: none;
  padding: 0;
}

.task-list li {
  margin: 10px 0;
}

.task-list a {
  color: #007bff; /* Warna biru untuk link */
  text-decoration: none; /* Menghilangkan garis bawah */
}

.task-list a:hover {
  text-decoration: underline; /* Menambahkan garis bawah saat hover */
}
</style>