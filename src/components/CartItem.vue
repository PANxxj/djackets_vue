<template>
    <tr>
        <td><router-link :to="item.product.get_absolute_url">{{ item.product.name }}</router-link></td>
        <td>Rs.{{ item.product.price }}</td>
        <td>{{ item.quantity }}</td>
        <td>Rs.{{ getItemTotal(item).toFixed(2) }}</td>
        <td><button class="delete"></button></td>
    </tr>

</template>

<script>
export default {
    name:'CarItem',
    props:{
        initialItem:Object
    },
    data(){
        return {
            item : this.initialItem
        }
    },
    methods:{
        getItemTotal(item){
            return this.item * item.product.price
        }
    }
}
</script>