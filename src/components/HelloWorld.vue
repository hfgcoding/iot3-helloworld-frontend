<template>
  <div class="hello" v-if="apidata !== null">
    <h1>API says: <pre>{{apidata.msg}}</pre></h1><br/><br/>
    <h2>And whats secret? <pre>{{apidata.secret}}</pre></h2>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'HelloWorld',
  data: function() {
    return {
      apidata: null
    }
  },
  props: {
    msg: String
  },
  mounted() {
    if(process.env.NODE_ENV === "development") {
      console.log("Lokaler Endpoint - Entwicklung")
      axios.get("http://localhost:3000/api/v1/hello").then((res)=>{
        this.apidata = res.data
      }).catch((e) => console.log(e))
    } else {
      console.log("Remote Endpoint - Container")
      axios.get("https://helloapi.ds.ava.hfg.design/api/v1/hello").then((res)=>{
        this.apidata = res.data
      }).catch((e) => console.log(e))
    }
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
</style>
