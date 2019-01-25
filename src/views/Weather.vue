<template>
    <div id="weather">
        <br>

        <section class="container">
            <div class="row">
                <div class="col-12" style="text-align:center;">
                    <h1>Weather Status</h1>
                </div>
            </div>
            <div class="dropdown-divider bg-secondary"></div>
            <br>
            <!-- <div class="row">
                <div class="col-md-9 col-12">
                    <div class="input-group mb-3">
                        <div class="input-group-prepend">
                            <span class="input-group-text bg-secondary text-white" id="inputGroup-sizing-default">City</span>
                        </div>
                        <input type="text" class="form-control" aria-label="Default" aria-describedby="inputGroup-sizing-default" placeholder="Where are you?" v-on:keyup.enter="findCity" v-model="cityName">
                    </div>
                </div> 
                <div class="col-md-2 offset-md-1 col-12">
                    <button type="button" class="btn btn-secondary btn-block" v-on:click="findCity">Find It</button>
                    <br>
                </div>        
            </div> -->
            <div class="row">
                <div class="col-12" style="text-align:center;">
                    <ul>
                        <li v-for="post in posts" style="list-style:none;">
                            <h3><b>{{ post.name }}</b></h3>
                        </li>
                    </ul>
                </div>
            </div>

            <button v-on:click="findCity"></button>

        </section> 
    <!-- <ul v-if="posts && posts.length">
        <li v-for="post of posts">
            <p><strong>{{post.title}}</strong></p>
            <p>{{post.body}}</p>
        </li>
    </ul> -->
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            posts: [],
            errors: [],
            cityName: "",
            city: ""
        }
    },
    methods: {
        findCity: function(){
            console.log(this.posts[0]);
        }
    },

  // Fetches posts when the component is created.
    created() {
    axios.get("http://api.openweathermap.org/data/2.5/weather?q=London&?units=metric&APPID=9788b3a9af1cfc6b792c28f70bea4579")
    .then(response => {
        // JSON responses are automatically parsed.
        this.posts = response.data
    })
        .catch(e => {
        this.errors.push(e)
    })

    // async / await version (created() becomes async created())
    //
    // try {
    //   const response = await axios.get(`http://jsonplaceholder.typicode.com/posts`)
    //   this.posts = response.data
    // } catch (e) {
    //   this.errors.push(e)
    // }
  }
}
</script>