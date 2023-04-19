<!-- <template>
  <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </nav>
  <router-view/>
</template> -->
<template>
    <el-menu
      :default-active="activeIndex"
      class="el-menu-demo"
      mode="horizontal"
      :ellipsis="false"
      @select="handleSelect"
    >
    <div class="nav">
      <el-menu-item index="0">LOGO</el-menu-item>
      <div class="navLinks">
        <el-menu-item index="1"><router-link to="/">Home</router-link></el-menu-item>
        <el-menu-item index="2"><router-link to="/buy">Buy</router-link></el-menu-item>
        <el-menu-item index="3"><router-link to="/sell">Sell</router-link></el-menu-item>
      </div>
      <div class="conn">
        <el-button style="margin-top: 8%;" type="primary">Connect</el-button>
      </div>
      <div class="burger">
        <a @click="toggle" ><img src="https://cdn3.iconfinder.com/data/icons/arrows-160/96/menuSmall-512.png"></a>
      </div>
    </div>
     <div class="burgerLinks">
        <el-menu-item index="1"><router-link to="/">Home</router-link></el-menu-item>
        <el-menu-item index="2"><router-link to="/buy">Buy</router-link></el-menu-item>
        <el-menu-item index="3"><router-link to="/sell">Sell</router-link></el-menu-item>
     </div>    
      
    </el-menu>
    <router-view/>
  
  </template>
  
  <script setup>
  import { ref } from 'vue';
 
  
  
  const activeIndex = ref('1');
  const handleSelect = (key, keyPath) => {
    console.log(key, keyPath);
  }
  
  const toggle = ()=>{
    let burgerlinks= document.getElementsByClassName("burgerLinks")[0];
    if(burgerlinks.style.display=='block'){
      burgerlinks.style.display= 'none';
    }
    else{
      burgerlinks.style.display= 'block';
    }
  }
  
  </script>
  
  <style>


  .nav {
    display: flex;
    justify-content: space-around;
  }
  .navLinks{
      display: flex;
  }
  .burger{
    display: none;
  }
  .burgerLinks{
    display: none;
  }
  a { 
    text-decoration: none; 
  }
  
  img{
    width: 50px;
    height: 50px;
  }
   
  @media only screen and (max-width:600px){
    .navLinks{
      display: none;
    }
    .burger{
      display: block;
    }
  }
  
  </style>
  
  
  