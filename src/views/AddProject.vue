<template>
    <div>
        <Navbar />
        <form @submit="handleSubmit">
            <label for="title" class="uppercase"> Title </label>
            <input type="text" v-model="title" name="title" required>
            <label for="details" class="uppercase "> Details </label>
            <textarea name="details" id="" cols="30" rows="10" v-model="details"></textarea>
            <button > Add Project</button>
        </form>
    </div>
</template>
<script>
import Navbar from '@/components/Navbar.vue'

export default {
    components:{
        Navbar
    },
   data(){
       return {
           title: '',
           details: '',
       }
   },
   methods:{
       handleSubmit(e){
       e.preventDefault();
        let project = {
            title : this.title,
            details: this.details,
            complete: false,
        }
        fetch( 'http://localhost:3000/projects', {
            method: 'POST',
            headers: { 'Content-Type' :  'application/json' },
            body: JSON.stringify( project )
        } )
        .then(() => {
            console.log( 23123)
            this.$router.push('/')
        }).catch( (err) => { console.log( err )})
       }
   }
}
</script>
<style scoped>
form{
    background: #fff;
    padding: 20px;
    border-radius:10px;
    margin: 20px auto;
}
label{
    display: block;
    color: #bbb;
    text-transform: uppercase;
    font-size: 14px;
    font-weight: bold;
    letter-spacing: 1px;
    margin: 20px 0px 10px 0px;
}
input{
    padding:10px;
    border:0;
    border-bottom: 1px solid #ddd;
    width: 100%;
    box-sizing: border-box;
}
textarea{
    border: 1px solid #ddd;
    padding:10px;
    width: 100%;
    box-sizing: border-box;
}
form button{
    display: block;
    margin: 20px auto 0;
    background: #00ce89;
    color: #fff;
    padding:10px;
    border:0;
    border-radius: 6px;
    font-size: 16px;
}
</style>