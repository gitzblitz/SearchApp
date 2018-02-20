<template>
    <div class="container">
        <h1>
            Search for Candidate
        </h1>

        <div class="well well-sm">
            <div class="form-group">
                <div class="input-group input-group-md">
                    <div class="icon-addon addon-md">
                        <input type="text" placeholder="Search for candidate..." class="form-control" v-model="query">
                    </div>
                    <span class="input-group-btn">
                        <button class="btn btn-default" type="button" @click="search()" v-if="!loading">Search!</button>
                        <button class="btn btn-default" type="button" disabled="disabled" v-if="loading">Searching...</button>
                    </span>
                </div>
            </div>
        </div>
        <div class="alert alert-danger" role="alert" v-if="error">
            <span class="glyphicon glyphicon-exclamation-sign" aria-hidden="true"></span>
            {{ error }}
        </div>
        <div id="candidates" class="row list-group">
            <div class="item col-xs-4 col-lg-4" v-for="candidate in candidates" :key="candidate.id">
                <div class="thumbnail">
                    <img class="group list-group-image" :src="candidate.profile_image" :alt="candidate.name" />
                    <div class="caption">
                        <h4 class="group inner list-group-item-heading">{{ candidate.name }}</h4>
                        <p class="group inner list-group-item-text">{{ candidate.biography }}</p>
                        <div class="row">
                            <div class="col-xs-12 col-md-6">
                                <star-rating :star-size="20" :rating="candidate.rating"></star-rating>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

</template>

<script>
import axios from 'axios'
import StarRating from 'vue-star-rating/src/star-rating'

export default {
  components: {StarRating},
  name: 'search',
  data: function () {
    return {
      candidates: [],
      loading: false,
      error: false,
      query: ''
    }
  },
  methods: {
    search: function () {
      this.error = ''
      this.candidates = []
      this.loading = true
      axios.get('http://localhost:8000/api/search?q=' + this.query, { crossdomain: true })
        .then(response => {
          response.data.error ? this.error = response.data.error : this.candidates = response.data
          this.loading = false
          this.query = ''
        }).catch(e => {
          this.error.push(e)
        })
    }
  }
}
</script>
