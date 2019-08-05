<template>
  <div>
    <div class="mainContainer">
      <form @submit.prevent="onClick" class="form">
        <div class="box-1">
          <h2>Search Book</h2>
        </div>
          <hr>
        <div class="box-2">
          <input type="text" v-model.trim="inputedPhrase" placeholder="⌕">
        </div>
          <hr>
        <div class="box-1">
          <button type="submit" class="button">Do it!</button>
        </div>
      </form>
    </div>
   <div class="mainContainer">
        <ul>
            <li v-for="result in results.items" :key="result.id" class="form">
                <div class="box-3">
                <img :src="result.volumeInfo.imageLinks.smallThumbnail">
                </div>
                <hr>
                <div class="box-3">
                <h3>{{ result.volumeInfo.title }}</h3>
                </div>
                <hr>
                <div class="box-3">
                <h4>{{ result.volumeInfo.description | cut }}...</h4>
                </div>
            </li>
        </ul>  
    </div>
  </div>
</template>
            

<script>
import axios from 'axios';
export default {
  data: () => {
    return {
            inputedPhrase: '',
            results:[]
           
  }
},
 methods:{
        onClick () {
            axios.get('https://www.googleapis.com/books/v1/volumes?q=' + this.inputedPhrase + '&maxResults=20&printType=all&projection=full')
            .then(response => {this.results = response.data})
            .catch(error => {console.log(error)})
        }
    } ,
 filters:{
   cut: (value) => {
     value = value.toString()
     return value.substr(0, 100)
   }
 }
}
</script>


<style>
.form{
    background-color: wheat;
    border-radius: 10px;
}
.results{
    display: flex;
    justify-content: center;
    flex-direction: column;
    border: 1px solid black;
}
body {
  background-color: rgb(54, 52, 49);
  margin: 0;
}
h2{
    font-weight: 300;
}
h3,h4{
    font-weight: 400;
}
.mainContainer
{
    margin: 50px 0px 80px 0px;
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
}
.box-1{
    display: flex;
    padding: 15px;
    justify-content: center;
}
.box-2{
    display: flex;
    padding: 15px;
}

.box-3{
    display: flex;
    padding: 15px;
    justify-content: center;
    width: 60vw;
    margin: 10px;
}
.button {
  display: inline-block;
  padding: 10px 15px;
  font-size: 16px;
  cursor: pointer;
  text-align: center;
  text-decoration: none;
  outline: none;
  color: #fff;
  background-color: #4CAF50;
  border: none;
  border-radius: 15px;
  box-shadow: 0 9px #999;
}

.button:hover {background-color: #3e8e41}

.button:active {
  background-color: #3e8e41;
  box-shadow: 0 5px #666;
  transform: translateY(4px);
}
img {
    flex: none;
    width: 6rem;
    height: auto;
    align-self: flex-start;
  }
  ul{
      list-style: none;
  }
</style>
