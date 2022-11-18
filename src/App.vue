<template>

    <div class="row m-2">
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
        <div class="col">
            <div class="d-flex flex-wrap">
                <div v-for="lesson of sortedLessons" :key="lesson.id" class="lesson-card-comp col m-3 p-3 border">
                    <div class="row">
                        <div class="col-8">
                            <div>
                                <strong>Subject: </strong>
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
                        <button class="btn btn-secondary" @click="add(lesson.id)">Add to card</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

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
                        <button class="btn btn-secondary" @click="remove(lesson.id)">Remove</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <div class="row m-2">
        <h2 class="text-center checkout">Checkout</h2>
        <div class="d-flex flex-wrap justify-content-center">
            Name:
            <label class="form-text-label m-2">
                <input class="form-text-input" type="text" name="order" />
            </label>
            <label class="form-text-label m-2">
                Phone
                <input class="form-text-input" type="text" name="order" />
            </label>
            <Button class="btn btn-success m-2">Checkout</Button>
        </div>
    </div>
</template>

<script>

import lessons from "./data/lessons";

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
            this.shoppingCartLessons

            for (let i = 0; i < this.shoppingCartLessons.length; i++) {
                if (this.shoppingCartLessons[i].id == id) {
                    if (this.shoppingCartLessons[i].spaces <= 1) {
                        this.shoppingCartLessons = []
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
        sortedLessons() {
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
