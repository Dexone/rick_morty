<template>
    <div id="block">
        <img id="photo" :src=cardInfo.image>
        <section style="font-size: 25px; margin-top: 10px;">{{ cutName(cardInfo.name) }}</section>
        <section style="font-size: 18px; margin-bottom: 10px;">{{ cardInfo.status }}-{{ cardInfo.species }}</section>
        <section style="color: #9e9e9e;">Last known location:</section>
        <section style="font-size: 18px; margin-bottom: 10px;">{{ cardInfo.location }}</section>
        <section style="color: #9e9e9e;">Gender:</section>
        <section style="font-size: 18px;">{{ cardInfo.gender }}</section>
        <section style="font-size: 18px;">{{ cardInfo.id }}</section>
    </div>
</template>

<script setup>
defineProps({
    cardInfo: {
        type: Object,
        required: true
    }
})
function cutName(name) {
    if (name.length > 16) {
       return name.split("").splice(0, 16).join("") + "..."
    }
    return name
}
</script>