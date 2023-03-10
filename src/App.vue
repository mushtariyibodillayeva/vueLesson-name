<template>
  <div class="box">
    <h1>APIga so'rov yuboring</h1>
    <div v-if="loading">Ma'lumotlar yuklanmoqda...</div>
    <div v-else-if="error">Xatolik yuz berdi: {{ error }}</div>
    <div v-else>
      <h2>{{ country.name }}</h2>
      <p>Asl nomi: {{ country.nativeName }}</p>
      <p>Aholi soni: {{ country.population }}</p>
      <p>Asosiy vaqti: {{ country.timezones[0] }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loading: true,
      error: null,
      country: null,
    };
  },
  created() {
    fetch("https://restcountries.com/v2/name/Uzbekistan")
      .then((response) => response.json())
      .then((data) => {
        this.country = data[0];
        this.loading = false;
      })
      .catch((error) => {
        console.log(error);
        this.error = "Ma'lumotlar yuklashda xatolik yuz berdi";
        this.loading = false;
      });
  },
};
</script>
