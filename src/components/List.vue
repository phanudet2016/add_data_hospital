<template>
  <div id="app">
    <p><router-link to="/">หน้าเพิ่มข้อมูล</router-link></p>
    <div class="containerr">
      <div class="TTT">
        <table class="table table-bordered">
                <thead>
                  <tr>
                    <th width="100px;" style="text-align: center;">ลำดับ</th>
                    <th width="500px" style="text-align: center;">ชื่ออุปกรณ์</th>
                    <th width="500px" style="text-align: center;">ชื่อภาษาอังกฤษ</th>
                    <th width="350px" style="text-align: center;">ราคา (ต่อหน่วย)</th>
                    <th width="800px" style="text-align: center;">คำอธิบาย</th>
                    <th width="350px" style="text-align: center;">ประเภทเครื่องมือแพทย์</th>
                    <th width="350px" style="text-align: center;">รหัส สนย.</th>
                    <th width="350px" style="text-align: center;">รหัส สงป.</th>
                    <th width="350px" style="text-align: center;">ระดับ สถานบริการ</th>
                    <th width="100px;" style="text-align: center;">ลบ</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="(data, index) of datas" v-bind:key="data['.key']">
                    <td>{{index+1}}.</td>
                    <td>{{data.nameTH}}</td>
                    <td>{{data.nameEng}}</td>
                    <td>{{data.unitPrice}}</td>
                    <td>{{data.description}}</td>
                    <td>{{data.categoryData}}</td>
                    <td>{{data.codeSNY}}</td>
                    <td>{{data.codeSNP}}</td>
                    <td>{{data.placeLevel}}</td>
                    <td><span @click="removeData(data['.key'])" class="glyphicon glyphicon-trash" style="color:red;"></span></td>
                  </tr>
                </tbody>
              </table>
      </div>
    </div>
  </div>
</template>

<script>
import {dataRef} from './firebase'

export default {
  name: 'list',
  data () {
    return {
      categoryData: ''
    }
  },
  firebase: {
    datas: dataRef
  },
  methods: {
    removeData (key) {
      dataRef.child(key).remove()
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
input[type=text], select {
    width: 100%;
    padding: 12px 20px;
    margin: 8px 0;
    display: inline-block;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
}

button {
    width: 100%;
    background-color: #4CAF50;
    color: white;
    padding: 14px 20px;
    margin: 8px 0;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

input[type=submit]:hover {
    background-color: #45a049;
}

.containerr {
    border-radius: 5px;
    background-color: #ffffff;
    padding: 20px;
    margin: 0px auto;
    width: 100%;
}

</style>
