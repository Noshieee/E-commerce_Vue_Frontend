<template>

<section>
  <div class="Intro">
    <h1 class="display-1">Kicking n Screaming</h1>
  </div>
  <p>
    All your Football needs, wants, and more...
  </p>

<router-link :to="{ name: 'Login' }"><button type="button" class="btn btn-primary btn-lg">Log in</button></router-link>
<router-link :to="{ name: 'Register' }"><button type="button" class="btn btn-secondary btn-lg">Sign up</button></router-link>
</section>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    login() {
      console.log(this.email, this.password);
      fetch("https://enosh-e-commerce-final-project.herokuapp.com/users", {
      method: "PATCH", 
      body: JSON.stringify({
        email: this.email, 
        password: this.password
        }), 
        headers: {
        "Content-Type": "application/json; charset=UTF-8"
        },
        })
        .then((response) => response.json())
        .then((json) => alert(json))
        .catch((e) => alert(e.msg))
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

section{
    height: 100vh;
    background-image: url('https://i.postimg.cc/0jkgz8rn/1952506.jpg  ');
    background-position: center;
    background-size: cover;
    background-repeat: no-repeat;
}
main {
  padding: 0 !important;
}

.Intro{
  padding-top: 200px;
  margin-top: auto;
  margin-bottom: auto;

}

h1{
  color: rgb(225, 0, 255);
  /* font-size: 100px; */
}

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
  color: rgb(225, 0, 255);
  text-decoration: none;
}
button {
  margin: 10px;
}

p {
  font-size: 40px;
  color: white;
}


</style>

