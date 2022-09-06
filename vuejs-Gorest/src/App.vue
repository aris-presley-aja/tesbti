<template>
    <div class="container">
        <div id="page">
            <transition name="fade">
                <router-view></router-view>
                <div v-for="post in filteredPosts" :key="post.id">
  <post :post="project"></post>
</div>
            </transition>
        </div>
    </div>
</template>

<style>
  .wrapper {
    display: flex;
    max-width: 444px;
    flex-wrap: wrap;
    padding-top: 12px;
  }


    .fade-enter-active, .fade-leave-active {
      transition: opacity .5s
    }
    .fade-enter, .fade-leave-active {
      opacity: 0
    }
    #app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  
}

@import'~bootstrap/dist/css/bootstrap.css'
</style>

<script>

    export default{
        data(){
            return{

            }
        }
    }
</script>
