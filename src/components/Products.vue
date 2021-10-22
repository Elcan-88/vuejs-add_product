<template>
    <div v-if="productList.length > 0">
        <h3 class="text-center">Eklenen Ürünlerin Listesi</h3>
        <hr>
        <div class="row product-container">
        <Product v-for="product in productList" :key="product">
                <img class="card-img-top" :src="product.selectedImage" alt="Card image cap">
                <div class="card-body">
                    <h5 class="card-title">{{ product.title }}</h5>
                    <small>
                        <strong>Adet : </strong> {{ product.count }}
                    </small>
                    <br>
                    <small>
                        <strong>Fiyat : </strong> {{ product.price }}
                    </small>
                    <br>
                    <small>
                        <strong>Tutar : </strong> {{ product.totalPrice }}
                    </small>
                </div>
        </Product>
        </div>
    </div>
</template>

<script>
import { eventBus } from "../main.js";
import Product from "./Product";
export default {
    components: {
        Product
    },
    data() {
        return{
            productList: []
        }
    },
    created() {
        eventBus.$on("productAdded", (product) => {
            this.productList.push(product);
            eventBus.$emit("progressBarUpdate", this.productList.length);
        });
    }
}
</script>