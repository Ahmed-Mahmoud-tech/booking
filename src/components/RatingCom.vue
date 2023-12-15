<template>
    <div class="rating">
        <span v-for="star in 5" :key="star" :class="{ 'lit': star <= rating }">&#9733;</span>
    </div>
</template>

<script>
export default {
    props: {
        rating: {
            type: Number,
            required: true,
        },
    },
};
</script>

<style scoped>
.rating {
    font-size: 24px;
}

.lit {
    color: gold;
}
</style>