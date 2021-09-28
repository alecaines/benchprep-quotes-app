<template>
  <div class="quotes">
    <div class = "controls">
      <div class = "search">
        <input id="query" type="text" placeholder="I'll be there in ten...">&nbsp;
        <button class="search-button" v-on:click="$data.temp = return_query($data)">search</button>
      </div>
      <div class="pagination">
          <button class = "pagination-button" v-on:click="$data.pageNumber > 0 ? $data.pageNumber-=1 : $data.pageNumber-=0">previous</button>&nbsp;&nbsp;
          <button class = "pagination-button" v-on:click="$data.temp.length > 15*($data.pageNumber+1) ? $data.pageNumber+=1 : $data.pageNumber+=0">next</button>
      </div>
      <div class="filters">
          <button class = "filter-button" v-on:click="$data.temp = movies($data);$data.pageNumber=0">Movies</button>&nbsp;&nbsp;<br>
          <button class = "filter-button" v-on:click="$data.temp = games($data);$data.pageNumber=0">Games</button>&nbsp;&nbsp;<br>
          <button class = "filter-button" v-on:click="$data.temp = $data.payload;$data.pageNumber=0">All</button>&nbsp;&nbsp;<br>
      </div>
    </div>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    <br>
    <div class="quotes-page scroll">
      <div class = "quotes-data">
          <ul>
                <li v-for="datum in $data.temp.slice(15*$data.pageNumber,15*($data.pageNumber+1) )" v-bind:key="datum.quote">
                    <div class="quote">
                        <h2>Source: {{datum.source}}</h2><br> 
                        Context: <i>{{datum.context}}</i><br>
                        Quote: "{{datum.quote}}"<br>
                        Theme: {{datum.theme}}<br>
                    </div>
                    <br>
                </li>
          </ul>
      </div>
    </div>
  </div>
</template>


<script>
import quotes from '../../quotes.json'

export default {
  name: 'Quotes',
  data (){
    return {
            payload: quotes, 
            temp: quotes,
            pageNumber: 0
          }
  },
  methods: {
    movies: (data) => {
      return data.payload.filter((datum) => datum.theme === "movies")
    },
    games: (data) => {
      return data.payload.filter((datum) => datum.theme === "games")
    },
    return_query: (data) => {
      const query = document.getElementById('query').value.toLowerCase();
      return data.payload.filter((datum) => datum.source.toLowerCase().includes(query) || datum.context.toLowerCase().includes(query) || datum.quote.toLowerCase().includes(query))
    }
  },
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.search{
  margin: 2%;
}

.filters{
  margin: 2%;
  align-content: center;

}

.pagination {
  padding: 4%;
  margin:2%;
}

input {
  font-family: 'Didact Gothic';
  border-radius: 5px;
  border: 2 !important;
  box-shadow: none! important;
}

button {
  border-radius: 5px;
  padding: 5%;
  opacity: 0.8;
  transition: 0.3s;
}

button:hover{
  opacity: 1;
}

.search-button {
  background-color: #e0dede;
  border: none;
  /* padding: 2%; */
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  cursor: pointer;
  margin:15%;
  font-family: 'Didact Gothic';
}

.pagination-button {
  background-color: #e8ae1a;
  border: none;
  color: white;
  /* padding: 2%; */
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  cursor: pointer;
}

.filter-button {
  background-color: #e8ae1a;
  border: none;
  color: white;
  /* padding: 2%; */
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  cursor: pointer;
  margin:1%;
}

.quotes {
    font-family: 'Didact Gothic';
    padding-left: 20%;
    padding-right: 20%;
    display:flex; 
    flex-direction: row;
    justify-content: center;
    align-items: center
}

.quote {
  background-color:white;
  padding: 10%;
  border-radius: 25px;
}

.quotes-data {
  background-color:#f7f5f5;
  padding: 25px;
  border-radius: 25px;

}

.quotes-page {
  border: black;
  border-width: 2px;
  outline-color: black;
  padding: 10%;
  height:300px;
  border-radius: 25px;
  background-color:#f2f0f0;
  }

.quotes-page.scroll {
  overflow-y: auto;
  overflow-x: hidden;
}
</style>
