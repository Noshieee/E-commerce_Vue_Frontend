<template>
  <div v-if="product">

  </div>
  
  <div v-else>Loading the product...</div>
        <div class="card">
        <img src="product.img" class="card-img-top" alt="${product.title}">
        <div class="card-body">
            <h5 class="card-title">{{product.title}}</h5>
            <h5 class="card-category">{{product.category}}</h5>
            <p class="card-text">R{{product.price}}</p>
          <div class="d-flex mb-3">
            <input type="number" class="form-control" value=1 min=1 id="addToCart${position}">
            <button type="button" class="btn btn-secondary ms-3" onclick="addToCart(${position})"><i class="bi bi-bag-plus"></i></button>
          </div>
        </div>
        </div>
</template>
<script>
export default {
  props: ["id"],
  data() {
    return {
      product: null,
    };
  },
  methods: {
        showCartBadge() {
      document.querySelector("#badge").innerHTML = cart ? cart.length : "";
    },
     addToCart(position) {
      let qty = document.querySelector(`#addToCart${position}`).value;
      let added = false;
      cart.forEach((product) => {
        if (product.title == products[position].title) {
          alert(
            `You have successfully added ${qty} ${products[position].title} to the cart`
          );
          product.qty = parseInt(product.qty) + parseInt(qty);
          added = true;
        }
      });
      if (!added) {
        cart.push({ ...products[position], qty });
        alert(
          `You have successfully added ${qty} ${products[position].title} to the cart`
        );
      }
    
      showCartBadge();
    
      localStorage.setItem("cart", JSON.stringify(cart));
    }
  },
  mounted() {
    fetch("https://enosh-e-commerce-final-project.herokuapp.com/products" + this.id, {
      method: "GET",
      headers: {
        "Content-type": "application/json; charset=UTF-8",
        Authorization: `Bearer ${localStorage.getItem("jwt")}`,
      },
    })
      .then((response) => response.json())
      .then(async (json) => {
        this.product = json;
        await fetch(
          "https://enosh-e-commerce-final-project.herokuapp.com/users" + json.title,
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
            this.product.title = json.name;
          });
      });
  },
};
</script>
<style>
.product {
  display: flex;
  flex-direction: column;
  padding: 0 10%;
  margin-inline: auto;
  align-items: stretch;
  gap: 30px;
}
.product-image {
  padding: 10px;
  width: 100%;
  min-width: 100%;
  max-height: 50vh;
  object-fit: cover;
}
.product-details {
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: left;
  gap: 8px;
}

.products-container {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  margin-inline: auto;
  padding: 30px;
  gap: 2%;
  justify-content: stretch;
  align-items: stretch;
}
.neu-border {
  border-radius: 30px;
  background: #f5f5f5;
  box-shadow: 8px 8px 15px #e4e4e4, -8px -8px 15px #ffffff;
}
.neu-border-inset {
  border-radius: 30px;
  background: #f5f5f5;
  box-shadow: inset 8px 8px 15px #e4e4e4, inset -8px -8px 15px #ffffff;
}
@media screen and (max-width: 500px) {
  .product {
    flex-direction: column;
  }
  .product-image,
  .product-details {
    width: 100%;
  }

  .product-details {
    align-items: flex-start;
    text-align: left;
  }
}

#products {
  flex-wrap: wrap;
  gap: 20px;
}

img {
  height: 200px !important;
  object-fit: cover;
}

.card {
  width: calc((100% / 4) - 15px);
  min-width: 300px;
}

.card-title {
  text-transform: capitalize;
}

</style>
