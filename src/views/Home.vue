<template>
  <div class="container mx-auto">
    <NavBar />
    <FilterNav msg="Welcome to Your Vue.js App" @updateFilter="updateFilter" :current="current" />
    <div v-if="projects.length" class= "w-6/12 mx-auto" >
      <div v-for="project in filteredProject" :key="project.id " >
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
      projects : [],
      current : 'all'
    }
  },
  methods:{
    updateFilter( by ){
      console.log( by )
        this.current = by
    },
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

console.log( this.projects)
    },
    getJsonData(){
      fetch('http://localhost:3000/projects')
        .then( res => res.json())
        .then( data => this.projects = data )
        .catch( err => console.log( console.log( 1 )))
    }
  },
  computed:{
    filteredProject(){
       switch(  this.current ){
        case 'ongoing':
           return this.projects.filter( project => !project.complete )
        break;
        case 'all':
          return this.projects 
        break;
        case 'completed':
          console.log( this.projects)
           return this.projects.filter( project => project.complete )
        break;
      }
    }
  },
  mounted(){
    this.getJsonData()
  }
}
</script>
