<template>
  <div class="container mx-auto">
    <NavBar />
    <FilterNav msg="Welcome to Your Vue.js App"/>
    <div v-if="projects.length" class= "w-6/12 mx-auto" >
      <div v-for="project in projects" :key="project.id " >
        <SingleProject :project="project" @deleteProject="handleDeleteProject"  @handleDeleteProject="handleDeleteProject"  @handleCompleteProject="handleCompleteProject" />
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import FilterNav from '@/components/FilterNav.vue'
import SingleProject from '@/components/Project.vue'
import NavBar from '@/components/Navbar.vue'

export default {
  name: 'Home',
  components: {
    FilterNav,
    SingleProject,
    NavBar
  },
  data(){
    return {
      projects : []
    }
  },
  methods:{
    handleDeleteProject( id ){
      console.log( id  )
      this.projects = this.projects.filter( (project) => {
       return  project.id !== id
      })
      console.log()
    },
    handleCompleteProject( id ){
      let p =  this.projects.find( project => {
        return project.id === id
      })
      
      p.complete =  !p.complete

    },
    getJsonData(){
      fetch('http://localhost:3000/projects')
        .then( res => res.json())
        .then( data => this.projects = data )
        .catch( err => console.log( console.log( 1 )))
    }
  },
  mounted(){
    this.getJsonData()
  }
}
</script>
