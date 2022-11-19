<template>
    <div class="row m-2">
        <Lessons :lessons="sorted" :add="(id) => { add(id) }" />

        <div class="col-sm-2 my-5">
            <div class="row">
                <h5>Sort by</h5>
                <label class="form-check-label">
                    <input class="form-check-input" type="radio" name="sort-by" v-model="sortWith" value="subject" />
                    Subject
                </label>
                <label class="form-check-label">
                    <input class="form-check-input" type="radio" name="sort-by" v-model="sortWith" value="location" />
                    Location
                </label>
                <label class="form-check-label">
                    <input class="form-check-input" type="radio" name="sort-by" v-model="sortWith" value="price" />
                    Price
                </label>
                <label class="form-check-label">
                    <input class="form-check-input" type="radio" name="sort-by" v-model="sortWith" value="spaces" />
                    Availability
                </label>
            </div>
            <div class="row mt-5">
                <label class="form-check-label">
                    <input class="form-check-input" type="radio" name="order" v-model="orderWith" value="asc" />
                    Ascending
                </label>
                <label class="form-check-label">
                    <input class="form-check-input" type="radio" name="order" v-model="orderWith" value="desc" />
                    Descending
                </label>
            </div>
        </div>
    </div>


    <ShoppingCart :shoppingCartLessons="shoppingCartLessons" :callback="(id) => { remove(id) }" />

    <Checkout :len="shoppingCartLessons.length" :callback="() => { shoppingCartLessons = [] }" />

</template>

<script>
import lessons from "./data/lessons";
import Checkout from "./Checkout.vue"
import ShoppingCart from "./ShoppingCart.vue"
import Lessons from "./Lessons.vue";

export default {
    name: "App",
    data() {
        return {
            lessons: lessons,
            shoppingCartLessons: [],
            sortWith: "subject",
            orderWith: "asc",
        };
    },
    components: {
        Checkout: Checkout,
        ShoppingCart: ShoppingCart,
        Lessons
    },
    methods: {
        add(id) {
            this.lessons.find((lesson) => {
                if (lesson.id == id && lesson.spaces > 0) {
                    let { ...newlesson } = lesson
                    lesson.spaces--
                    newlesson.spaces = 1
                    let done = this.shoppingCartLessons.find((slesson) => {
                        if (slesson.id == id) {
                            slesson.spaces++
                            return true
                        }
                    })
                    if (!done) {
                        this.shoppingCartLessons.push(newlesson)
                    }
                }
            })
        },
        remove(id) {
            for (let i = 0; i < this.shoppingCartLessons.length; i++) {
                if (this.shoppingCartLessons[i].id == id) {
                    if (this.shoppingCartLessons[i].spaces <= 1) {
                        this.shoppingCartLessons.splice(i)
                    } else {
                        this.shoppingCartLessons[i].spaces--;
                    }
                    this.lessons.find((lesson) => {
                        if (lesson.id == id) {
                            lesson.spaces++
                            return true
                        }
                    })
                }
            }
        }
    },
    computed: {
        sorted() {
            if (this.lessons.length < 1) return this.lessons;

            let sortwith = this.sortWith ?? "subject";
            let ordwith = this.orderWith ?? 'asc';

            return this.lessons.sort(function (a, b) {
                let aa = ordwith === "asc" ? a : b;
                let bb = ordwith === "asc" ? b : a;
                if (typeof aa[sortwith] === "number") {
                    return (aa[sortwith] - bb[sortwith]);
                } else {
                    return ((aa[sortwith] < bb[sortwith]) ? -1 : ((aa[sortwith] > bb[sortwith]) ? 1 : 0));
                }
            });
        },
    },
};

</script>
<style>
.lesson-card-comp {
    max-width: 15rem;
    border-radius: 1rem;
}

.lesson-card-comp button {
    width: fit-content;
    border-radius: 5px;
    padding: 0 1.5rem;
}

.checkout,
.shopping-cart {
    min-height: 10rem;
}
</style>
