<template>
  <div id="app">
    <p><router-link to="/list">รายการข้อมูล</router-link></p>
    <img src="../assets/logo.png" width="400px">
    <div class="container">
      <div class="inputData">
        <form action="/action_page.php">
          <input type="text" placeholder="ชื่ออุปกรณ์" v-model="nameTH"/>
          <input type="text" placeholder="ชื่อภาษาอังกฤษ" v-model="nameEng"/>
          <input type="text" placeholder="ราคา (ต่อหน่วย)" v-model="unitPrice"/>
          <input type="text" placeholder="คำอธิบาย (เฉพาะรายการที่เป็นชุด หรือมีชื่อที่ไม่ชัดเจน เช่น ชุด ระดับ)" v-model="description"/>
          <select id="country" name="country" v-model="categoryData">
            <option disabled value="">ประเภทเครื่องมือแพทย์</option>
            <option>รักษา</option>
            <option>วินิจฉัย</option>
            <option>วินิจฉัยและรักษา</option>
            <option>รักษาชีวิต</option>
            <option>สนับสนุน</option>
            <option>รถพยาบาล</option>
            <option>รถยนต์/รถจักรยานยนต์/รถอื่นๆ</option>
            <option>ไฟฟ้าและวิทยุ</option>
            <option>การศึกษา</option>
            <option>สำนักงาน</option>
          </select>
          <input type="text" placeholder="รหัส สนย." v-model="codeSNY"/>
          <input type="text" placeholder="รหัส สงป." v-model="codeSNP"/>
          <input type="text" placeholder="ระดับ สถานบริการ" v-model="placeLevel"/>
          <button @click="submitData()" type="button" data-dismiss="modal">ตกลง</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import {dataRef} from './firebase'

export default {
  name: 'home',
  data () {
    return {
      categoryData: ''
    }
  },
  firebase: {
    datas: dataRef
  },
  methods: {
    submitData () {
      dataRef.push({
        nameTH: this.nameTH,
        nameEng: this.nameEng,
        unitPrice: this.unitPrice,
        description: this.description,
        categoryData: this.categoryData,
        codeSNY: this.codeSNY,
        codeSNP: this.codeSNP,
        placeLevel: this.placeLevel
      })
    },
    removeEqm (key) {
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
    background: #4CAF50;
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

.container {
    border-radius: 5px;
    background-color: #ffffff;
    padding: 20px;
    margin: 0px auto;
    width: 960px;
}

</style>
