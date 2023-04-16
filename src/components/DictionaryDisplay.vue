<template>
    <div class="word d-flex justify-content-between align-items-center" v-if="data">
      <div>
        <h2 class="word__title">{{ data.word }}</h2>
        <h3 class="word__pronounciation" v-if="data.phonetic">{{ data.phonetic }}</h3>
        <h3 class="word__pronounciation" v-if="data.phonetics[1]" v-show="!data.phonetic">{{ data.phonetics[1].text }}</h3>
      </div>
      <div>
        <button class="play" v-if="data.phonetics[1]" v-show="data.phonetics[1].audio" @click="playAudio">
            <audio :src="data.phonetics[1].audio" id="audio"></audio>
            <img src="../assets/play.png" alt="">
        </button>
        <button class="play" v-if="data.phonetics[0]" v-show="!data.phonetics[1]" @click="playAudio2">
            <audio :src="data.phonetics[0].audio" id="audio2"></audio>
            <img src="../assets/play.png" alt="">
        </button>
      </div>
    </div>

    <!-- Definitions -->
    <div class="definitions" v-if="data" v-for="meaning in data.meanings">
        <div class="def">
            <div class="def__category">
                <h3 class="name">{{ meaning.partOfSpeech }}</h3>
                <div class="line"></div>
            </div>
            <!-- Meanings -->
            <h3 class="title">Meaning</h3>
            <ul>
                <li v-for="def in meaning.definitions">
                    {{ def.definition }}
                </li>
            </ul>
            <!-- Synoyms -->
            <div class="def__synonyms" v-if="meaning.synonyms.length > 0">
                <h3 class="title">Synoyms</h3>
                <h3 class="synonym" v-for="synonym in meaning.synonyms">{{ synonym }}</h3>
            </div>
        </div>       
    </div>
    <!-- Source Link -->
    <div class="definitions__source" v-if="data">
        <div class="line"></div>
        <h3>Source</h3>
        <a :href="data.sourceUrls[0]" target="_blank">{{ data.sourceUrls[0] }}</a>
    </div>

    <!-- Not found Section -->
    <div class="not-found" v-if="!data">
        <h1>Word not found.</h1>
    </div>
</template>

<script>
export default {
    props: ['data'],
    methods: {
        playAudio() {
            audio.play();
        },
        playAudio2() {
            audio2.play();
        }
    }
}
</script>

<style lang="scss" scoped>
@use '../scss/variables' as var;

// Line
.line {
    top: 0;
    left: 0;
    right: 0;
    position: absolute;
    height: 1px;
    background: #E0E0E0;
}

// Word Section
.word {
  &__title {
    font-size: var.$fs-accent-50;
  }

  &__pronounciation {
    font-size: var.$fs-title-40;
    font-weight: 400;
    font-family: Inter, sans-serif !important;
    color: var.$clr-accent-purple;
  }

  .play {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 75px;
    height: 75px;
    border-radius: 50%;
    border: none;
    cursor: pointer;
    transition: all 0.2s;
    background: var.$clr-lt-purple;

    &:active {
      opacity: 70%;
    }

    img {
      width: 46px;
    }
  }
}

.definitions {
    .def {
        padding-top: 40px;

        &__category {
            position: relative;
            margin-bottom: 35px;
            
            .line {
                top: 50%;
                left: 140px;
            }
            .name {
                font-size: var.$fs-title-40;
                font-style: italic;
                color: var.$clr-txt-dark;
                font-weight: 700;
            }
        }

        .title {
            font-size: var.$fs-title-30;
            color: var.$clr-txt-grey;
            font-weight: 400;
        }

        ul {
            padding-left: 30px;
            padding-top: 20px;
            font-size: var.$fs-txt-20;
            color: var.$clr-txt-dark;

            li {
                padding: 5px 0;
            }
        }

        &__synonyms {
            padding-top: 35px;
            display: flex;
            align-items: center;
            flex-wrap: wrap;

            .title {
                padding-right: 15px;
            }
            
            .synonym {
                color: var.$clr-accent-purple;
                padding: 5px 15px;
                padding-left: 0;
            }
        }
    }

    &__source {
        position: relative;
        display: flex;
        align-items: center;
        padding-top: 20px;
        padding-bottom: 120px;
        margin-top: 50px;

        h3 {
            padding-right: 30px;
            font-weight: 400;
            color: var.$clr-txt-grey;
            font-size: var.$fs-txt-10;
        }

        a {
            color: var.$clr-txt-dark;
            font-size: var.$fs-txt-10;

            &:hover {
                text-decoration: none;
            }
        }
    }
}
</style>