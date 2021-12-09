<template>
  <div id="content">  
  <h1>...</h1>  
    <div>
      <label>Product Name</label> : <input type="text" id="txt1" v-model="model.productName"  />
    </div>
    <div>
      <label>Desciription</label> : <input type="text" id="txt2" v-model="model.descrption" />
    </div>
       
    <div>
      <button type="button" v-on:click="saveClick">Save</button>
    </div>
  </div>
  <hr />
  <hr />
  <h1>...</h1>
  <table border="1" style="margin:auto">
    <thead>
      <tr>
        <th style="width: 100px">ID</th>
        <th style="width: 100px">Product Name</th>
        <th style="width: 100px">Desciription</th>       
        <th style="width: 100px"></th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="item in model.list" v-bind:key="item.id">
        <td>{{ item.id }}</td>
        <td>{{ item.productName }}</td>
        <td>{{ item.descrption }}</td>      
        <td><button type="button" v-on:click="deleteClick(item.id)">Delete</button></td>
      </tr>
    </tbody>
  </table>
</template>

<script>
import axios from "axios";

export default {
  name: "Product",
  data: function () {
    return {
      model: {
        productName: "",
        descrption: "",
        
      },
      list: [],
    };
  },
  methods: {
    saveClick() {      
      axios
        .post("http://example.com", this.model)
        .then((resp) => {
          this.getList();
          alert("success" + resp.data.id);
        });
    },
    getList() {
      axios.get("http://example.com").then((resp) => {
        this.model.list = resp.data;        
      });
    },
    deleteClick(id) {
      axios.delete("http://example.com" + id).then(() => {
         this.getList();
         alert("success");  
      });
    }
  },  
  mounted: function () {
    this.getList();
  },
};
</script>
