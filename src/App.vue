<template>
  <div class="all">
    <p class="atasan">Selamat Datang...</p>
    <br>
    <p style="
      position: absolute;
      font-size: 25px;
      padding-left: 500px;">
      Tabel Daftar Buku
    </p>
    <p style="
      font-size: 25px;
      padding-left: 70px">Form Peminjaman Buku</p>
    <table align= "center"
    style="width: 700px;
          position: absolute;
          margin-left:500px;
          margin-top:10px;">
      <thead>
      <tr>
      <th>No</th>
      <th>Nama Siswa</th>
      <th>Judul Buku</th>
      <th>Tanggal Pinjam</th>
      <th>Tanggal Pengembalian</th>
      </tr>
      </thead>
      <tbody>
        <tr v-for="user in users" :key="user.idd">
          <td class="centerin">{{user.id}}</td>
          <td>{{user.siswa}}</td>
          <td class="centerin">{{user.buku}}</td>
          <td>{{user.tpinjam}}</td>
          <td>{{user.tkembali}}</td>
          <td style="
          width: 20px;
          background-color: rgb(106, 193, 224);"><button style="width:100px"
          type="button" class="btn btn-outline-primary" role="button" @click="edit(user)">Perpanjang</button>
           <button type="button" class="button-55" @click="del(user)">Kembali</button></td>
        </tr>
      </tbody>
      </table>
    <form @submit.prevent="add">
        <div id="app">
        <label for="Nama Siswa">Nama Siswa</label><br>
        <input class="inpstyle" required
        type="text" v-model="form.siswa">
        <br>
        <label for="Judul Buku">Judul Buku</label><br>
        <input class="inpstyle" required
        type="text" v-model="form.buku">
        <br>
        <label for="Tahun Pinjam">Tanggal Pinjam</label><br>
        <input class="inpstyle" required
        type="date" v-model="form.tpinjam">
        <br>
        <label for="Tanggal Pengembalian">Tanggal Pengembalian</label><br>
        <input class="inpstyle" required
        type="date" v-model="form.tkembali">
        </div>
        <br>
        <button type="submit" style="margin-left: 70px; width: 400px;"
        class="button-54" role="button" v-show="!updateSubmit">Add Peminjaman</button>
        <button type="button" style="margin-left: 70px; width: 400px;"
        class="button-54" role="button" v-show="updateSubmit" @click="update(form)">Perbarui Daftar Pinjaman</button> 
    </form>
</div>
</template>
<script>
/* eslint-disable */ 
import axios from 'axios'
export default {
  data(){
    return{
        form: {
          id: '',
          siswa: '',
          buku: '',
          tpinjam: '',
          tkembali: ''
        },
        users: '',
        updateSubmit: false
    }
  },
  mounted() {
    this.load()
  },
  methods: {
    load(){
        axios.get('http://localhost:3000/users').then(res => {
        this.users = res.data
      }).catch ((err) => {
        console.log(err);
        
      })
    },add() {
      axios.post("http://localhost:3000/users/", this.form).then((res) => {
        this.load();
        this.form.id = "";
        this.form.siswa = "";
        this.form.buku = "";
        this.form.tpinjam = "";
        this.form.tkembali = "";
      });
    },
    edit(user) {
      this.updateSubmit = true;
      this.form.id = user.id;
      this.form.siswa = user.siswa;
      this.form.buku = user.buku;
      this.form.tpinjam = user.tpinjam;
      this.form.tkembali = user.tkembali;
    },
    update(form) {
      return axios
        .put("http://localhost:3000/users/" + form.id, {
          id: this.form.id,
          siswa: this.form.siswa,
          buku: this.form.buku,
          tpinjam: this.form.tpinjam,
          tkembali: this.form.tkembali,
        })
        .then((res) => {
          this.load();
          this.form.id = "";
          this.form.siswa = "";
          this.form.buku = "";
          this.form.tpinjam = "";
          this.form.tkembali = "";
          this.updateSubmit = false;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    del(user) {
      axios.delete("http://localhost:3000/users/" + user.id).then((res) => {
        this.load();
        let index = this.users.indexOf(form.name);
        this.users.splice(index, 1);
      })
    }
  }
}
</script>

<style>
.all {
  background-color: rgb(106, 193, 224);

}
.atasan {
  text-align: center;
  padding-top: 20px;
  font-size: 30px;
}
td {
  background-color: white;
  border: solid skyblue 1px;
}
.centerin {
  text-align: center;
}
.inpstyle {
  width: 400px;
  text-align: center;
  padding-left: 30px;
}
#app {
  margin-left: 70px;
}
.button-55 {
  align-self: center;
  background-color: #fff;
  background-image: none;
  background-position: 0 90%;
  background-repeat: repeat no-repeat;
  background-size: 5px 4px;
  border-radius: 15px 225px 255px 15px 15px 255px 225px 15px;
  border-style: solid;
  border-width: 3px;
  box-shadow: rgba(0, 0, 0, .2) 15px 28px 25px -18px;
  box-sizing: border-box;
  color: #41403e;
  cursor: pointer;
  display: inline-block;
  font-family: Neucha, sans-serif;
  font-size: 1rem;
  line-height: 23px;
  outline: none;
  padding: .75rem;
  text-decoration: none;
  transition: all 235ms ease-in-out;
  border-bottom-left-radius: 15px 255px;
  border-bottom-right-radius: 225px 15px;
  border-top-left-radius: 255px 15px;
  border-top-right-radius: 15px 225px;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  background-color: skyblue;
  width: 100px;
}

.button-55:hover {
  box-shadow: rgba(0, 0, 0, .3) 2px 8px 8px -5px;
  transform: translate3d(0, 2px, 0);
}

.button-55:focus {
  box-shadow: rgba(0, 0, 0, .3) 2px 8px 4px -6px;
}
.button-54 {
  font-family: "Open Sans", sans-serif;
  font-size: 16px;
  letter-spacing: 2px;
  text-decoration: none;
  text-transform: uppercase;
  color: #000;
  cursor: pointer;
  border: 3px solid;
  padding: 0.25em 0.5em;
  box-shadow: 1px 1px 0px 0px, 2px 2px 0px 0px, 3px 3px 0px 0px, 4px 4px 0px 0px, 5px 5px 0px 0px;
  position: relative;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
}

.button-54:active {
  box-shadow: 0px 0px 0px 0px;
  top: 5px;
  left: 5px;
}

@media (min-width: 768px) {
  .button-54 {
    padding: 0.25em 0.75em;
  }
}
</style>