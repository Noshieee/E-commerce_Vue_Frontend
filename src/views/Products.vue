<template>
  <div v-if="products">
    <h2>Products</h2>

  </div>
  <div v-else>Loading products...</div>
    <div class="container d-flex justify-content-end mb-3 mt-5 pt-4">
      <div class="d-flex w-25 ms-3">
        <label for="" class="form-label">Sort by category</label>
        <select
          class="form-select"
          v-model="selected"
          name=""
          id="sortCategory"
          @change="sortCategory()"
        >
          <option value="All">All</option>
          <option value="Footwear">Footwear</option>
                <option value="Clothing">Clothing</option>
                <option value="Accessories">Accessories</option>
        </select>
      </div>
      <div class="d-flex w-25 ms-3">
        <label for="" class="form-label">Sort name</label>
        <select class="form-select" name="" id="sortName" @change="sortName()">
          <option value="ascending">Ascending</option>
          <option value="descending">Descending</option>
        </select>
      </div>
      <div class="d-flex w-25 ms-3">
        <label for="" class="form-label">Sort price</label>
        <select
          class="form-select"
          name=""
          id="sortPrice"
          @change="sortPrice()"
        >
          <option value="ascending">Ascending</option>
          <option value="descending">Descending</option>
        </select>
      </div>
    </div>
    
          <div class="row">
            <div class="card col-sm-3 col-3" v-for="product in products" :key="product.id">
              <div v-if="products" >
                <img :src="product.img" class="card-img-top" alt="${product.title}">
                <div class="card-body">
                  <h5 class="card-title">{{ product.title }}</h5>
                  <h5 class="card-category">{{ product.category }}</h5>
                  <p class="card-text">R{{ product.price }}</p>
                </div>
                  <!-- <div class="d-flex mb-3">
                    <input type="number" class="form-control" value=1 min=1 id="addToCart${position}">
                    <button type="button" class="btn btn-secondary ms-3" onclick="addToCart({{position}})"><i class="bi bi-bag-plus"></i></button>
                  </div> -->
              </div>
            </div>      
         </div>


</template>
<script>
export default {
  data() {
    return {
      products: null,
    };
  },
      methods: {
      sortName() {
      let direction = document.querySelector("#sortName").value;
    
      let sortedProducts = products.sort((a, b) => {
        if (a.title.toLowerCase() < b.title.toLowerCase()) {
          return -1;
        }
        if (a.title.toLowerCase() > b.title.toLowerCase()) {
          return 1;
        }
        return 0;
      });
      if (direction == "descending") sortedProducts.reverse();
      console.log(sortedProducts);
      readProducts(products);
    },
      sortPrice() {
      let direction = document.querySelector("#sortPrice").value;
    
      let sortedProducts = products.sort((a, b) => a.price - b.price);
    
      console.log(sortedProducts);
    
      if (direction == "descending") sortedProducts.reverse();
      readProducts(sortedProducts);
    },
      },
    mounted() {
      if (localStorage.getItem("jwt")) {
        fetch("https://enosh-e-commerce-final-project.herokuapp.com/products", {
          method: "GET",
          headers: {
            "Content-type": "application/json; charset=UTF-8",
            Authorization: `Bearer ${localStorage.getItem("jwt")}`,
          },
        })
          .then((response) => response.json())
          .then((json) => {
            this.products = json;
            this.products.forEach(async (product) => {
              await fetch(
                "https://enosh-e-commerce-final-project.herokuapp.com/users" + product.title,
                {
                  method: "GET",
                  headers: {
                    "Content-type": "application/json; charset=UTF-8",
                    Authorization: `Bearer ${localStorage.getItem("jwt")}`,
                  },
                }
              )
                .then((response) => response.json())
                .then((json) => {
                  product.title = json.name;
                });
            });
          })
          .catch((err) => {
            alert("User not logged in");
          });
      } else {
        alert("User not logged in");
        this.$router.push({ name: "Login" });
      }
    },
}
</script>

<style scoped>




#products {
  gap: 20px;
}

img {
    height: 200px !important;
  object-fit: cover;
  max-width: 200px 
}

.card {
  width: calc((100% / 4) - 15px);
  min-width: 250px;
  margin-left: 10px;
  margin-bottom: 10px;
  align-items: center;
  padding-bottom: 50px;
}

.card-title {
  text-transform: capitalize;
}

.form-label {
  color: rgb(182, 22, 22);
}
</style>