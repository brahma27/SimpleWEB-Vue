<template>
    <div class="row" >
        <div
            class="card border-1 ml-2"
            style="width: 15rem;margin-left:10px;margin-top:10px;"
            v-for="item in produk"
            :key="item.id"
            >
            <img src="../assets/logo.png" class="card-img-top" />
            <div class="card-body">
                <p class="card-title" style="font-weight: bold;">{{item.title}}</p>
                <p class="card-text">{{item.body}}</p>
                <button type="button" class="btn btn-warning" v-on:click="deleteData(item.id)">Remove</button>
            </div>
        </div>
        
  </div>
</template>

<script>
import Vue from 'vue'
import axios from "axios";
import VueAxios from 'vue-axios'
Vue.use(VueAxios,axios)
export default{
    name:"Body",
    data() 
    {
        return{produk:null}
    },
    methods:{
        getData()
        {
            this.axios.get("https://jsonplaceholder.typicode.com/posts")
                .then((response) => {
                    // console.log(response)
                    this.produk=response.data
            })
        },
        deleteData(id)
        {
            this.axios.delete("https://jsonplaceholder.typicode.com/posts/"+id).then((response)=>{
                console.warn(response)
                this.getData();
            })
        }
    },
    mounted() {
        this.getData()
    },
}
</script>
