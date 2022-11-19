<script>
export default {
    name: "Checkout",
    data() {
        return {
            name: "",
            phone: "",
        };
    },
    props: ['len', 'callback'],
    methods: {
    checkout() {
        if (this.name === '' || this.phone === '') {
            alert("Enter name and phone.")
            return
        }
        if (this.len < 1) {
            alert("Add lessons to cart.")
            return
        }
            alert(this.name + ", Your order placed.")
            this.name = ''
            this.phone = ''
        this.callback()
        }
    }
    }
    </script>

<template>
    <div class="row m-2">
        <h2 class="text-center checkout">Checkout</h2>
        <div class="d-flex flex-wrap justify-content-center">
            Name:
            <label class="form-text-label m-2">
                <input class="form-text-input" type="text" v-model="name" />
            </label>
            <label class="form-text-label m-2">
                Phone
                <input class="form-text-input" type="text" v-model="phone" />
            </label>
            <Button class="btn btn-success m-2" @click="checkout()">Checkout</Button>
        </div>
    </div>
</template>

<style scoped>
</style>
