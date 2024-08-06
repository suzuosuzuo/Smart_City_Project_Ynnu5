<!-- 地球自转 -->
<template>
    <div>
    </div>
</template>
<script setup>
import { inject, onMounted, onBeforeUnmount } from "vue";
let map, scene;
onMounted(() => {
    ({ map, scene } = inject('mapScene'));
    console.log(map, scene);
    rotate();
    map.on("moveend", rotate);
});
function rotate() {
    let center = map.getCenter();
    center.lng += 1;
    map.easeTo({
        center,
        duration: 500,
        zoom: 1,
        pitch:0,
        bearing: 0,
        easing: (n) => n,
    });
}
onBeforeUnmount(() => {
    map.off("moveend", rotate);
    map.stop();
});
</script>
<style scoped></style>
