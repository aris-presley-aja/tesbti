<template>
    <div id="all-products">
        <h1>All Data</h1>
         <!-- <p><router-link :to="{ name: 'create_product' }" class="btn btn-primary">Create Data</router-link></p> -->

<!-- <input class="form-control" type="text" id="" onkeyup="searchedProducts()" placeholder="Search.." title="Type in"> -->
        <div class="form-group">
    <input type="text" name="search" v-model="productSearch" placeholder="Search" class="form-control" v-on:keyup="searchedProducts()">


        </div>

        <table id="tgj" class="table table-hover">
            <thead>
            <tr>
                <td>ID</td>
                <td>User ID</td>
                <td>Title</td>
                <td>Body</td>
                <td>Actions</td>

            </tr>
            </thead>

            <tbody>


                    <!-- <td>{{ product.id }}</td> -->
                    <td>{{ product.title }}</td>
                    <td>{{ product.createdBy }}</td>

                    <td>{{ product.body }}</td>
                    <td>
                        <router-link :to="{name: 'edit_product', params: { id: product.id }}" class="btn btn-primary">Edit</router-link>
                        <router-link :to="{name: 'delete_product', params: { id: product.id }}" class="btn btn-danger">Delete</router-link>
                    </td>
                    <!--  -->

                    <!--  -->
 
                
            </tbody>
        </table>
    </div>
</template>

<script>
 

    export default{
          components: {
    
  },
    
 
        data()
        {
            return{
                filter: "",
                search: "",
                products: [],

          selectVal: {

      id: undefined,
      user_id: undefined,
      title: undefined
    }
                
            }
            
        },

        created: function()
        {
            this.fetchProductData();

        },
// 

// Add computed section:

//  
        methods: {
            fetchProductData: function()
            {
                this.$http.get('https://bti.id/services/btiportalcorems/api/pt-job-posts/no-auth').then((response) => {
                    this.products = response.body;
                    this.originalProducts = this.products;
                }, (response) => {

                });
            },
        },
// 
    }   
 
// 
    //             searchProducts: function()
    //         {
    //             if(this.productSearch == '')
    //             {
    //                 this.products = this.originalProducts;
    //                 return;
    //             }

    //             var searchedProducts = [];
    //             for(var i = 0; i < this.originalProducts.length; i++)
    //             {
    //                 var productName = this.product[i]['name'].toLowerCase();
    //                 if(productName.indexOf(this.productSearch.toLowerCase()) >= 0 )
    //                 {
    //                     searchedProducts.push(this.searchedProducts[i]);
    //                 }
    //             }

    //             this.products = searchedProducts;
    //         }
    //     }
        
    // }
</script>
