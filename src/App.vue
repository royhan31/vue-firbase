<template>
  <div id="app">
    <v-container class="grey lighten-5">
      <v-app>
       <v-row>
         <v-col cols="9">
           Data Mahasiswa
           <v-simple-table>
            <template v-slot:default>
              <thead>
                <tr>
                  <th class="text-left">No</th>
                  <th class="text-left">Nim</th>
                  <th class="text-left">Nama</th>
                  <th class="text-left">Email</th>
                  <th class="text-left">Aksi</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(student,no) in students" :key="student.id">
                  <td>{{no+1}}</td>
                  <td>{{student.nim}}</td>
                  <td>{{student.name}}</td>
                  <td>{{student.email}}</td>
                  <td>
                    <v-btn v-on:click="edit(student.id)" class="mx-2 mb-2" small
                    color="warning">Edit</v-btn>
                    <v-btn v-on:click="deleteData(student.id)" class="mx-2 mb-2" small
                    color="error">Hapus</v-btn>
                  </td>
                </tr>
              </tbody>
            </template>
          </v-simple-table>
         </v-col>
         <v-col cols="3">
           <v-card class="mx-auto" max-width="344" height="auto" outlined>
             <v-card-title>
               Tambah Mahasiswa
             </v-card-title>
             <v-card-actions>
                <v-row>
                  <v-col cols="12">
                    <div class="my-2">
                      <v-text-field mt-0 label="Nim" v-model="student.nim"
                      single-line outlined required>
                      </v-text-field>
                    </div>
                    <div class="my-2">
                      <v-text-field label="Nama" v-model="student.name"
                      single-line outlined required></v-text-field>
                    </div>
                    <div class="my-2">
                      <v-text-field label="Email" v-model="student.email"
                      single-line outlined required></v-text-field>
                    </div>
                    <div class="my-2 text-center">
                      <v-btn v-if="!actionEdit" v-on:click="store"
                      class="mx-2 mb-2" color="info">Tambah</v-btn>
                      <v-btn v-if="actionEdit" v-model="student.id" v-on:click="update"
                      class="mx-2 mb-2" color="warning">Update</v-btn>
                      <v-btn v-if="actionEdit" v-on:click="cancel"
                      class="mx-2 mb-2" color="error">Batal</v-btn>
                    </div>
                  </v-col>
                </v-row>
             </v-card-actions>
          </v-card>
         </v-col>
       </v-row>
     </v-app>
     </v-container>
  </div>
</template>
<script>
import firebase from './firebase';

const database = firebase.ref('students');

export default {
  name: 'App',
  data() {
    return {
      actionEdit: false,
      student: {
        nim: '',
        name: '',
        email: '',
      },
      students: [],
    };
  },

  methods: {
    cancel: function cancel() {
      this.actionEdit = false;
      this.student.nim = '';
      this.student.name = '';
      this.student.email = '';
    },
    store: function store() {
      database.push(this.student);
      this.student.nim = '';
      this.student.name = '';
      this.student.email = '';
    },
    edit: function edit(id) {
      const data = this.students.find(student => student.id === id);
      this.student.nim = data.nim;
      this.student.name = data.name;
      this.student.email = data.email;
      this.student.id = data.id;
      this.actionEdit = true;
    },
    update: function update() {
      database.child(this.student.id).update(this.student);
      this.cancel();
    },
    deleteData: function deleteData(id) {
      database.child(id).remove();
    },
  },
  created() {
    database.on('child_added', data => this.students.push({ ...data.val(), id: data.key }));
    database.on('child_changed', (data) => {
      const updateStudent = this.students.find(student => student.id === data.key);
      updateStudent.nim = data.val().nim;
      updateStudent.name = data.val().name;
      updateStudent.email = data.val().email;
    });
    database.on('child_removed', (data) => {
      const deleteStudent = this.students.find(student => student.id === data.key);
      const index = this.students.indexOf(deleteStudent);
      this.students.splice(index, 1);
    });
  },
};
</script>
