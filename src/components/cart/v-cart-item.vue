<template>
    <div class="v-cart-item">
        <img class="v-cart-item__image" :src="require('../../assets/images/' + cart_item_data.image)" alt="img">
        <div class="v-cat-item__info">
            <p>{{cart_item_data.name}}</p>
            <p>{{cart_item_data.price}}</p>
            <p>{{cart_item_data.article}}</p>
        </div>
        <div class="v-cart-item__quantity">
            <p>Количество:</p>
            <span>
                <span class="quantity_btn" @click="decrementItem">-</span>
                {{cart_item_data.quantity}}
                <span class="quantity_btn" @click="incrementItem">+</span>
            </span>
        </div>
        <button @click="deleteFromCart">Удалить</button>
    </div>
</template>

<script>

    export default {
        name: "v-cart-item",
        props: {
            cart_item_data: {
                type: Object,
                default() {
                    return {}
                }
            }
        },
        data() {
            return {}
        },
        methods: {
            decrementItem() {
                this.$emit('decrement');
            },
            deleteFromCart() {
                this.$emit('deleteFromCart');
            },
            incrementItem() {
                this.$emit('increment')
            }
        },
        mounted() {
            this.$set(this.cart_item_data, 'quantity', 1)
        }
    }
</script>

<style lang="scss">
    .v-cart-item {
        display: flex;
        flex-wrap: nowrap;
        justify-content: space-between;
        align-items: center;
        box-shadow: 0 0 8px 0 #e0e0e0;
        padding: $padding*2;
        margin-bottom: $margin*2;
        .v-cart-item__image {
            width: 50px;
        }
        .quantity_btn {
            cursor: pointer;
        }
    }
</style>
