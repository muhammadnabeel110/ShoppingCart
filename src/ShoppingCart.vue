<script>
export default {
    name: "ShoppingCart",
    props: ['shoppingCartLessons', 'callback']

    }
    </script>

<template>
    <div class="row m-2">
        <h2 class="text-center m-3 shopping-cart">Shopping Cart</h2>
        <div class="col">
            <div class="d-flex flex-wrap">
                <div v-for="lesson of shoppingCartLessons" :key="lesson.id" class="lesson-card-comp col m-3 p-3 border">
                    <div class="row">
                        <div class="col-8">
                            <div>
                                <strong>Subject:</strong>
                                <span>{{ lesson.subject }}</span>
                            </div>
                            <div>
                                <strong>Location:</strong>
                                <span>{{ lesson.location }}</span>
                            </div>
                            <div>
                                <strong>Price:</strong>
                                <span>£{{ lesson.price }}</span>
                            </div>
                            <div>
                                <strong>Spaces:</strong>
                                <span>{{ lesson.spaces }}</span>
                            </div>
                        </div>

                        <div class="col-4">
                            <i :class="lesson.icon"></i>
                        </div>
                    </div>

                    <div class="d-flex justify-content-center mt-2">
                        <button class="btn btn-secondary" @click="callback(lesson.id)">Remove</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

</template>

<style scoped>
</style>
