<template>
    <div class="cart-page">
        <div class="columns is-multiline">
            <div class="column is-12">
                <h1 class="title">Cart</h1>
            </div>

            <div class="column is-12 box">
                <table class="table is-fullwidth" v-if="cartTotalLength">
                <thead>
                    <th>Product</th>
                    <th>Price</th>
                    <th>Quantity</th>
                    <th>Total</th>
                    <th></th>
                </thead>
                <tbody>
                    <CartItem 
                    v-for="item in cart.items"
                    v-bind:key="item.product.id"
                    v-bind:initialItem="item"
                    /> 
                </tbody>
                </table>
                <p v-else>you don not any products on you cart</p>
            </div>

            <div class="column is-12 box">
                <h2 class="subtitle">Summary</h2>

                <strong>Rs.{{ cartTotalPrice.toFixed(2) }}</strong>,{{ cartTotalLength }} items
                <hr>

                <router-link to="cart/checkout" class="button is-dark">Proceed to checkout</router-link>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import CartItem from '@/components/CartItem.vue'
export default {
    name:'Cart',
    components:{
        CartItem
    },
    data() {
        return {
            cart:{
                items:[]
            }
        }
    },
    mounted() {
        this.cart=this.$store.state.cart
    },
    computed:{
        cartTotalLength() {
            return this.cart.items.reduce((acc,curVal) => {
                return acc+=curVal.quantity
            },0)
        },
        cartTotalPrice() {
            return this.cart.items.reduce((acc,curVal) => {
                return acc+=curVal.quantity * curVal.product.price
            },0)
        }
    }
}
</script>