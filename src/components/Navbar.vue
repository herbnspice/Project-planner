<template>
    <div id="nav">
        <router-link to="/" class="text-color-gray-100">Projects </router-link> |
        <router-link to="/add">Add a new Project</router-link>
    </div>
</template>
<style scoped>
    #nav a{
        color: #999;
        margin: 0 10px;
        font-size: 18px;
        
    }
    a.router-link-active{
        border-bottom: 2px solid #00ce89;
        padding-bottom:4px;
    }
</style>