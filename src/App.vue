<template>
  <div id="app">
    <div class="myface">
      <img src="" alt="">

    </div>
    <div class="presentation">
      <i>"{{ quote }}"</i>
    <p>- Kanye West -</p>
    <p>
      <button @click="createPost">Create Post</button>
    </p>
    </div>
  </div>
  

 
</template>



<script>
import { ref } from 'vue'
import KanyeAPI from './services/KanyeAPI'

export default {
  setup() {

    const quote = ref('')

    const loadQuote = async () => {
      try {
        const response = await KanyeAPI.getQuote()
        quote.value = response.data.quote
      } catch (err) {
        console.log(err)
      }
    }

    loadQuote()

    const createPost = async () => {
      const response = await KanyeAPI.createPost(JSON.stringify({
        title: 'foo',
        body: 'bar',
        userId: 1,
      }))

        console.log(response)
  
    }

   

     return {
      createPost,
      quote
     }

  }
}





  //axios.get('https://api.kanye.rest/')
     //.then(response => {
      //quote.value = response.data.quote
     //})
</script>



<style >
#app {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  background-color: #111;
}
.presentation {
  display: flex;
  flex-wrap: wrap;
  flex-direction: column;
  gap: 2em;
  margin-top: 80px;
}
i  {
  color: #fff;
  font-size: 1.6em;
  font-weight: 600;
}
p {
  color: #fff;
  font-size: 1em;
  font-weight: 500;
}

</style>

