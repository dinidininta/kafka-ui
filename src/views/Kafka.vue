<template>
  <div class="about">
    <button @click="submitOrder">Order SLIK</button>
    <p v-for="(key, value) in Object.entries(matchingCustomer)" :key="key">{{key}} : {{value}}</p>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Kafka',
  data() {
    return {
      matchingCustomer: {},
    };
  },
  methods: {
    async submitOrder() {
      const payload = {
        Source: 'VUE',
        ReffNo: 'JF251019084207006996',
        Product: 'JF-J01',
        RequestData: [
          {
            individualid: '251019084207006996_25',
            status_app: 'DEBITUR',
            cust_name: 'YULI SETIAWAN',
            ktp: '3671062207740001',
            dob: '19740722',
            gender: 'L',
            pob: 'KULON PROGO',
            mother_name: 'SURABI',
            npwp: '550893010416000',
            homeaddress: 'PANINGGILAN UTARA NO 33',
            homecity: '0812',
            homezipcode: '15153',
            isCompany: '0',
            request_purpose: 'Penilaian Calon Debitur',
            nama_mitra: 'FMF',
            PIN: '04012119007389',
          },
        ],
      };
      try {
        await axios.post('http://localhost:3000/producer', payload);
        alert('Berhasil!');
      } catch (error) {
        alert('Gagal!');
      }
    },
  },
};
</script>
