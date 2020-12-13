<template>
  <div class="home">
    <div class="header">
        <input placeholder="Search for photo" type="text" name="" id="">
    </div>
    <div class=" grid-row">

      <div class="item1">

        <div class="upper">

          <button type="button" class="btn btn-lg" data-toggle="modal" data-target="#myModal" @click.prevent="modalImage = photos[1].small">
            <img class="rounded center" :src="photos[1].small" alt="" srcset=""> 
          </button>

             
          <div class="bottom-left">
            
            <a :href="photos[1].source_profile">
                  <p> {{ photos[1].source_name }} </p>
            </a>
            <p>{{ photos[1].location }}</p>
          </div>

        </div>

        <div class="lower">

          <button type="button" class="btn btn-lg" data-toggle="modal" data-target="#myModal">
            <img class="rounded" :src="photos[2].small" alt="" srcset="">
          </button>
        
          <div class="bottom-left">
            <a :href="photos[2].source_profile">
              <p> {{ photos[2].source_name }} </p>
            </a>
            <p>{{ photos[2].location }}</p>
          </div>

        </div>

      </div>
      
        

      <div class="item2">
        
        <div class="upper">
          <button type="button" class="btn btn-lg" data-toggle="modal" data-target="#myModal">
            <img class="rounded" :src="photos[3].small" alt="" srcset="">
          </button>

          <div class="bottom-left">
            <a :href="photos[3].source_profile">
              <p> {{ photos[3].source_name }} </p>
            </a>
            <p>{{ photos[3].location }}</p>
          </div>

        </div>

        <div class="lower">

          <button type="button" class="btn btn-lg" data-toggle="modal" data-target="#myModal">
            <img class="rounded" :src="photos[4].small" alt="" srcset="">
          </button>

          <div class="bottom-left">
            <a :href="photos[4].source_profile">
              <p> {{ photos[4].source_name }} </p>
            </a>
            <p>{{ photos[4].location }}</p>
          </div>

        </div>
      </div>

    

      <div class="item3">
        
        <div class="upper">

          <button type="button" class="btn btn-lg" data-toggle="modal" data-target="#myModal">
            <img class="rounded" :src="photos[5].small" alt="" srcset="">
          </button>

          <div class="bottom-left">
            <a :href="photos[5].source_profile">
              <p> {{ photos[5].source_name }} </p>
            </a>
            <p>{{ photos[5].location }}</p>
          </div>

        </div>

        <div class="lower">

          <button type="button" class="btn btn-lg" data-toggle="modal" data-target="#myModal">
            <img class="rounded" :src="photos[6].small" alt="" srcset="">
          </button>

          <div class="bottom-left">
            <a :href="photos[6].source_profile">
              <p> {{ photos[6].source_name }}</p>
            </a> 
              <p>{{ photos[6].location }}</p>
          </div>

        </div>
        
      </div>

    </div>
    Trigger the modal with a button
    <!-- <button type="button" class="btn btn-lg" data-toggle="modal" data-target="#myModal">Open Modal</button> -->

    <!-- Adding the modal component to template -->
    <Modal :modalImage="imageURL" />


    


  </div>
</template>

<script>


// @ is an alias to /src

import Unsplash, {toJson} from 'unsplash-js';
import Modal from '../components/modal'
export default {
  name: 'Home',
  components: {
    Modal
  },

  data() {
    return{  
    modev: process.env.VUE_APP_MODE,
    access: process.env.ACCESS_KEY,
    secret: process.env.SECRET_KEY,
    photos: [],
    modalImage: ''
    }
  },
  mounted() {
    // const unsplash = new Unsplash({ accessKey: this.access });
    const unsplash = new Unsplash({
      accessKey: 'pd60l4JwEiNhvLbdYbS3MIa-qpokzzbKEW0ybeMHf1g',
      secret: 'wAJkH_ctgMApPZOj_R0tY_EB86RQM0v8HVoHhLLUu6s'
    });
    
    unsplash.search.photos("dogs", 1, 10, { orientation: "portrait", color: "green" })
    .then(toJson)
    .then(json => {
      // Your code
      //  console.log(json.results)
      json.results.forEach(element => {
          let photo = {
          small: element.urls.small,
          large: element.urls.full,
          source_name: `${element.user.first_name}` +' '+ `${element.user.last_name ? element.user.last_name : ''}`,
          source_profile: `${element.user.links.html}` + `?utm_source=cowrywise-app&utm_medium=referral`,
          location: element.user.location
        }
        this.photos.push(photo)
      });
      console.log(this.photos)
    });
  }
}
</script>

<style  scoped>
.header {
  background-color: aquamarine;
  width: 100%;
}

.header input {
  width: 80%;
  margin: 4em;
  line-height: 2.5em;
  border-radius: 0.5em;
  border-style: none !important;
  font-size: 1.5em;
  padding: 0 1.5em;
  text-align: center;
  /* border: none !important; */
}
input:focus, textarea:focus, select:focus{
  outline: none;
}

a{
  padding: 0;
  margin: 0;
}
p {
  padding: 0;
}

.item1 {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  padding: 1em;
}

.item2 {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  padding: 1em;
}

.item3 {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  padding: 1em;
}

.grid-row {
  padding: 0 10em;
  display: flex;
  flex-direction: row;
  justify-content: center;
}

.grid-row img {
  display: block;
  width: 100%;
  max-width: 500px;
  min-width: 200px;
  margin-top: 1em;
  max-width: 200px;
}
.lower, .upper {
  position: relative;
  text-align: center;
  color: white;
  width: 100%;
}

.bottom-left {
  position: absolute;
  bottom: 1em;
  left: 2.9em;
}
a {
  color: white;
}

.grid-row {
  margin-top: -3em;
}
button {
  border: none;
  padding: 0;
  margin: 0;
}
img {
  transition: all 1s ease-in-out;
}
img:hover {
  transform: scale(1.3);
}

</style>