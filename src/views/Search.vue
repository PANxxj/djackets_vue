<template>
    <div class="page-search">
        <div class="columns is-multiline">
            <div class="column is-12">
                <h1 class="title">Search</h1>
                <h2 class="is-size-5 has-text-gray">Search term : {{ quary }}</h2>
            </div>
            <ProductBox
                v-for="product in latestproducts"
                v-bind:key="product.id"
                v-bind:product="product"
                />
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import ProductBox from '@/components/ProductBox.vue';
export default {
    name:'Search',
    components:{
        ProductBox,
    },
    data() {
        return {
            products:[],
            quary:''
        }
    },
    mounted() {
        document.title = 'Search | Djackets'

        let url=window.location.search.substring(1)
        let params=new URLSearchParams(url)

        if (params.get('quary')){
            this.quary=params.get('query')
            this.performSearh()
        }
    },
    methods:{
        
    }
}
</script>