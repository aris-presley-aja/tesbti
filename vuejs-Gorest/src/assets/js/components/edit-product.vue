<template>
    <div id="update-product">
        <h1>Update Product</h1>

        <p><router-link :to="{ name: 'all_products' }">Return to products</router-link></p>

        <notification v-bind:notifications="notifications"></notification>

        <form v-on:submit.prevent="editProduct">
            <div class="form-group">
                <label name="id">ID</label>
                <input type="text" class="form-control" disabled v-model="product.id" id="id">
            </div>

            <div class="form-group">
                <label name="user_id">Name</label>
                <input type="text" class="form-control" v-model="product.user_id" id="user_id" required>
            </div>

            <div class="form-group">
                <label name="title">Price</label>
                <input type="text" class="form-control" v-model="product.title" id="title" required>
            </div>

            <div class="form-group">
                <label name="body">body</label>
                <input type="text" class="form-control" v-model="product.body" id="body" required>
            </div>

            <div class="form-group">
                <button class="btn btn-primary">Update</button>
            </div>
        </form>
    </div>
</template>

<script>
    import Notification from './notifications.vue';

    export default{
        data(){
            return{
                product:{},
                notifications:[]
            }
        },

        created: function(){
            this.getProduct();
        },

        methods: {
            getProduct: function()
            {
                this.$http.get('https://gorest.co.in/public/v2/' + this.$route.params.id).then((response) => {
                    this.product = response.body;
                }, (response) => {

                });
            },

            editProduct: function()
            {
                // Validation
                var user_id = parseFloat(this.product.user_id);
                if(isNaN(user_id))
                {
                    this.notifications.push({
                        type: 'danger',
                        message: 'User ID must be a number'
                    });
                    return false;
                }

                this.$http.patch('https://gorest.co.in/public/v2/edit' + this.$route.params.id, this.product, {
                    headers : {
                        'Content-Type' : 'application/json'
                    }
                }).then((response) => {
                    this.notifications.push({
                        type: 'success',
                        message: 'Product updated successfully'
                    });
                }, (response) => {
                    this.notifications.push({
                        type: 'error',
                        message: 'Product not updated'
                    });
                });
            }
        },

        components: {
            'notification' : Notification
        }
    }
</script>
