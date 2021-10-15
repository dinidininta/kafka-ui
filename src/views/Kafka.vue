<template>
  <div class="about">
    <button @click="submitOrder">Order SLIK</button>
    <table>
      <thead>
        <td>Index</td>
        <td>Json</td>
      </thead>
      <tbody>
        <tr v-for="(result, index) in aggregationResult" :key="index">
          <td>{{index}}</td>
          <td>{{result.value}}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Kafka',
  data() {
    return {
      aggregationResult: {},
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
  async mounted() {
    const { data } = await axios.get('http://localhost:3000/consumer');
    this.aggregationResult = data.messages;
  },
};
</script>

<style>
  table, th, td {
    border: 1px solid black;
    border-collapse: collapse;
    margin-top: 25px;
  }
</style>
