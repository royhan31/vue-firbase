<template>
  <div class="row">
  <div class="column-1" >
    <h3>Data Mahasiswa</h3>
    <table>
  <tr>
    <th>No</th>
    <th>Nim</th>
    <th>Nama</th>
    <th>Email</th>
    <th>Jurusan</th>
    <th>Aksi</th>
  </tr>
  <tr>
    <td>Alfreds Futterkiste</td>
    <td>Alfreds Futterkiste</td>
    <td>Maria Anders</td>
    <td>Germany</td>
    <td>Germany</td>
    <td>
      <button type="button" class="btn-edit" name="button">Edit</button>
      <button type="button" class="btn-delete" name="button">Hapus</button>
    </td>
  </tr>
</table>
  </div>
  <div class="column-2" style="background-color:#bbb;">
   <h4>{{inputTitle}}</h4>
   <span>Nim</span>
   <input type="text" name="" value="">
   <span>Nama</span>
   <input type="text" name="" value="">
   <span>Email</span>
   <input type="text" name="" value="">
   <span>Jurusan</span>
   <select class="" name="">
     <option value="">Pilih Jurusan</option>
   </select>
   <button type="button" name="button">Tambah</button>
   <button type="button" name="button">Tambah</button>
  </div>
</div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      inputTitle: 'Tambah Mahasiswa',
    };
  },
};
</script>

<style scoped>
  * {
    box-sizing: border-box;
  }

.column-1 {
  float: left;
  width: 75%;
  padding: 10px;
  height: 100%;
}

.column-2 {
  float: left;
  width: 25%;
  padding: 10px;
  height: 100%;
}

.row:after {
  content: "";
  display: table;
  clear: both;
}

table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

td, th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}

input {
  display: block;
  margin-bottom: 4px;
  width: 300px;
  height: 30px;
}

select {
  display: block;
  margin-bottom: 4px;
  width: 200px;
  height: 30px;
}

button {
  /* display: block; */
  margin-top: 10px;
  background-color: blue;
  width: 100px;
  height: 50px;
  color: white;
  border-color: blue
}

.btn-edit {
  display: block;
  margin-top: 10px;
  background-color: orange;
  width: 40px;
  height: 20px;
  color: white;
  border-color: orange
}

.btn-delete {
  display: block;
  margin-top: 10px;
  background-color: red;
  width: 55px;
  height: 20px;
  color: white;
  border-color: red
}
</style>
