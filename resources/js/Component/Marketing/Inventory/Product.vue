<template>
    <Layout>
        <div class="justify-center w-full">
            <div class="flex justify-between items-end mt-6">
                <div class="mt-6 mb-6">
                    <span
                        class="text-xl font-bold text-gray-700 dark:text-gray-300"
                        >Pending Products</span
                    >
                </div>
            </div>
            <div class="overflow-x-auto border border-gray-300">
                <table
                    class="w-full text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400"
                >
                    <thead
                        class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400"
                    >
                        <tr>
                            <th scope="col" class="px-6 py-3">Image</th>
                            <th scope="col" class="px-6 py-3">Product Name</th>
                            <th scope="col" class="px-6 py-3">Category</th>
                            <th scope="col" class="px-6 py-3">Item Code</th>
                            <th scope="col" class="px-6 py-3">
                                Product Supplier
                            </th>
                            <th scope="col" class="px-6 py-3">Price</th>
                            <th scope="col" class="px-6 py-3">Quantity</th>
                            <th scope="col" class="px-6 py-3">Description</th>
                            <th scope="col" class="px-6 py-3">Status</th>
                            <th scope="col" class="px-20 py-3">Action</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr
                            v-for="product in pendingProducts"
                            :key="product.productId"
                            class="odd:bg-white odd:dark:bg-gray-900 even:bg-gray-50 even:dark:bg-gray-800 border-b dark:border-gray-700"
                        >
                            <td class="px-6 py-4">
                                <img
                                    :src="product.image"
                                    alt="Product Image"
                                    class="w-34 h-auto rounded-lg"
                                />
                            </td>
                            <th
                                scope="row"
                                class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white"
                            >
                                {{ product.productName }}
                            </th>
                            <td class="px-6 py-4">
                                <p>{{ getCategoryName(product.categoryId) }}</p>
                            </td>
                            <td class="px-6 py-4">{{ product.item_code }}</td>
                            <td class="px-6 py-4">{{ product.supplier }}</td>
                            <td class="px-6 py-4">{{ product.price }}</td>
                            <td class="px-6 py-4">{{ product.qty }}</td>
                            <td class="px-6 py-4">{{ product.description }}</td>
                            <td class="px-6 py-4">{{ product.status }}</td>
                            <td
                                class="px-6 py-4 flex justify-center items-center space-x-2"
                            >
                                <editProduct :product="product" />
                                <Approve :product="product" />
                                <button
                                    class="bg-red-500 px-2 py-2 rounded-md text-white my-2 text-sm hover:bg-green-600"
                                    @click="returnAll(product)"
                                >
                                    Return
                                </button>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>

            <div class="flex justify-between items-end mt-6">
                <div class="mt-6 mb-6">
                    <span
                        class="text-xl font-bold text-gray-700 dark:text-gray-300"
                        >Product List</span
                    >
                </div>
            </div>

            <div class="overflow-x-auto border border-gray-300">
                <table
                    class="w-full text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400"
                >
                    <thead
                        class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400"
                    >
                        <tr>
                            <th scope="col" class="px-6 py-3">Image</th>
                            <th scope="col" class="px-6 py-3">Product Name</th>
                            <th scope="col" class="px-6 py-3">Category</th>
                            <th scope="col" class="px-6 py-3">Item Code</th>
                            <th scope="col" class="px-6 py-3">
                                Product Supplier
                            </th>
                            <th scope="col" class="px-6 py-3">Price</th>
                            <th scope="col" class="px-6 py-3">Quantity</th>
                            <th scope="col" class="px-6 py-3">Description</th>
                            <th scope="col" class="px-6 py-3">Status</th>
                            <th scope="col" class="px-20 py-3">Action</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr
                            v-for="product in approvedProducts"
                            :key="product.productId"
                            class="odd:bg-white odd:dark:bg-gray-900 even:bg-gray-50 even:dark:bg-gray-800 border-b dark:border-gray-700"
                        >
                            <td class="px-6 py-4">
                                <img
                                    :src="product.image"
                                    alt="Product Image"
                                    class="w-34 h-auto rounded-lg"
                                />
                            </td>
                            <th
                                scope="row"
                                class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white"
                            >
                                {{ product.name }}
                            </th>
                            <td class="px-6 py-4">{{ product.cat_code }}</td>
                            <td class="px-6 py-4">{{ product.item_code }}</td>
                            <td class="px-6 py-4">{{ product.supplier }}</td>
                            <td class="px-6 py-4">{{ product.price }}</td>
                            <td class="px-6 py-4">{{ product.qty }}</td>
                            <td class="px-6 py-4">{{ product.description }}</td>
                            <td class="px-6 py-4">{{ product.status }}</td>
                            <td
                                class="px-6 py-4 flex justify-center items-center space-x-2"
                            >
                                <editProduct :product="product" />
                                <button
                                    class="bg-red-500 px-2 py-2 rounded-md text-white my-2 text-sm hover:bg-green-600"
                                    @click="product.productId;"
                                >
                                    Return
                                </button>
                                <Return :product="product" />
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </Layout>
</template>

<script>
import Modal from "@/Component/Modal.vue";
import editProduct from "@/Component/Marketing/inventory/editProduct.vue";
import Approve from "@/Component/Marketing/inventory/Approve.vue";
import Return from "@/Component/Marketing/inventory/Return.vue";

import axios from "axios";

export default {
    components: {
        Modal,
        editProduct,
        Approve,
        Return,
    },
    data() {
        return {
            pendingProducts: [],
            approvedProducts: [],
            editProduct: {
                item_code: "",
                productId: "",
                name: "",
                supplier: "",
                price: "",
                qty: "",
                description: "",
                status: 0,
            },
            products: [],
            categories: [],
            editingProductId: null,
            modalStatus: false,
        };
    },
    methods: {
        changeModalStatus() {
            this.modalStatus = !this.modalStatus;
        },

        getProducts() {
            axios.get("/get-products").then(({ data }) => {
                this.products = data;
            });
        },

        getPendingProducts() {
            axios.get("/get-products?status=0").then(({ data }) => {
                this.pendingProducts = data;
            });
        },
        getApprovedProducts() {
            axios.get("/get-products?status=1").then(({ data }) => {
                this.approvedProducts = data;
            });
        },

        getCategoryName(categoryId) {
            const category = this.categories.find(
                (cat) => cat.categoryId === categoryId
            );
            return category ? category.categoryName : this.categoryName;
        },

        getCategories() {
            axios.get("/get-categories").then(({ data }) => {
                this.categories = data;
            });
        },

        editProduct(product) {
            this.editProduct = { ...product };
            this.editingProductId = product.id;
            this.modalContent.title = "Edit Product";
            this.modalStatus = true;
        },

        updateProduct() {
            const { editProduct, editingProductId } = this;
            const prodPayload = { ...editProduct };

            axios
                .post("/update-product", { prodPayload, editingProductId })
                .then(({ data }) => {
                    if (prodPayload.status === 1) {
                        this.getProducts();
                    }
                })
                .catch((error) => {
                    console.error("Error updating product:", error);
                });
        },

        // returnAll(product) {
        //     const { editProduct, editingProductId } = this;
        //     const prodPayload = { ...editProduct };

        //     axios
        //         .post("/returnAll-product", { prodPayload, editingProductId })
        //         .then(({ data }) => {
        //             window.location.reload("Reloading");
        //         })
        //         .catch((error) => {
        //             console.error("Error updating product:", error);
        //         });
        // },
        returnAll(product) {
            axios
                .post("/returnAll-product", { product })
                .then(({ data }) => {
                    window.location.reload("Reloading");
                })
                .catch((error) => {
                    console.error("Error returning all products:", error);
                });
        },

        deleteProduct(productId) {
            axios.post("/delete-product", { productId }).then(({ data }) => {
                this.getProducts();
            });
        },
    },
    computed: {
        pendingProducts() {
            return this.products.filter((product) => product.status === 0);
        },
        approvedProducts() {
            return this.products.filter((product) => product.status === 1);
        },
    },
    mounted() {
        this.getProducts();
        this.getApprovedProducts();
        this.getPendingProducts();
        this.getCategories();
    },
};
</script>
