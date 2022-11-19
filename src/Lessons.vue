<script>
export default {
    name: "Lessons",
    props: ['lessons', 'add']
}
</script>

<template>

    <div class="col">
        <div class="d-flex flex-wrap">
            <div v-for="l of lessons" :key="l.id" class="lesson-card-comp col m-3 p-3 border">
                <div class="row">
                    <div class="col-8">
                        <div>
                            <strong>Subject: </strong>
                            <span>{{ l.subject }}</span>
                        </div>
                        <div>
                            <strong>Location:</strong>
                            <span>{{ l.location }}</span>
                        </div>
                        <div>
                            <strong>Price:</strong>
                            <span>£{{ l.price }}</span>
                        </div>
                        <div>
                            <strong>Spaces:</strong>
                            <span>{{ l.spaces }}</span>
                        </div>
                    </div>

                    <div class="col-4">
                        <i :class="l.icon"></i>

                    </div>
                </div>

                <div class="d-flex justify-content-center mt-2">
                    <button class="btn btn-secondary" @click="add(l.id)" :disabled="l.spaces < 1">Add to
                        card</button>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>

</style>
