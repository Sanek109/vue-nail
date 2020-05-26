<template>
    <div class="v-catalog">
        <router-link :to="{name: 'cart', params: {cart_data: CART}}">
            <div class="v-catalog__link_to_cart">Cart: {{CART.length}}</div>
        </router-link>
        <h1>Catalog</h1>
        <v-select
            :selected="selected"
            :options="categories"
            @select="sortCategories">

        </v-select>
        <div class="v-catalog__list">
            <v-catalog-item
                    v-for="product in filteredProducts"
                    :key="product.article"
                    :product_data="product"
                    @addToCart="addToCart"
            />
        </div>
    </div>
</template>

<script>
    import vCatalogItem from './v-catalog-item'
    import {mapActions, mapGetters} from 'vuex';
    import vSelect from '../v-select';

    export default {
        name: "v-catalog",
        components: {
            vCatalogItem,
            vSelect
        },
        props: {},
        data() {
            return {
                categories: [
                    {name: 'Все', value: 'Все'},
                    {name: 'Мужские', value: 'м'},
                    {name: 'Женские', value: 'ж'}
                ],
                selected: 'Все',
                sortedProducts: []
            }
        },
        computed: {
            ...mapGetters([
                'PRODUCTS',
                'CART'
            ]),
            filteredProducts() {
                if(this.sortedProducts.length) {
                    return this.sortedProducts
                } else {
                    return this.PRODUCTS
                }
            }
        },
        methods: {
            ...mapActions([
                'GET_PRODUCTS_FROM_API',
                'ADD_TO_CART'
            ]),
            sortCategories(category) {
                let vm = this;
                this.PRODUCTS.map(function(item) {
                    if(item.category === category.name) {
                        vm.sortedProducts.push(item)
                    }
                })
                this.selected = category.name
            },
            addToCart(data) {
                this.ADD_TO_CART(data)
            }
        },
        mounted() {
            this.GET_PRODUCTS_FROM_API().then(response => {
                if(response.data) {
                    console.log('Data arrive!')
                }
            })
        }
    }
</script>

<style lang="scss">
    .v-catalog {
        &__list {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            align-items: center;
        }
        &__link_to_cart {
            position: absolute;
            top: 10px;
            right: 10px;
            padding: $padding*2;
            border: solid 1px gray;
        }
    }
</style>
