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

</template>

<script>

import lessons from "./data/lessons";

export default {
    name: "App",

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
