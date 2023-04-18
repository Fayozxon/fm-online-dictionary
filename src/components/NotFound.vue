<template>
    <div class="box">
        <h2 class="emoji">🙄</h2>
        <h2 class="info">We cannot find the word you are looking for. Try searching another word.</h2>
    </div>
</template>

<script>

</script>

<style lang="scss" scoped>
@use '../scss/variables' as var;

.box {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    padding-top: 50px;

    .emoji {
        font-size: 64px;
        padding: 30px;
    }
    .info {
        text-align: center;
        width: 50%;
        font-size: 24px;
        font-family: Inter, sans-serif;
        font-weight: 400;
    }
}
/* RWD */
@media only screen and (max-width: 991px) {
    .info {
        width: 90% !important;
    }
}
// Dark Mode
body.dark {
    .info {
        color: var.$clr-white;
    }
}
</style>