<template>
 <header class="header">
    <div class="container d-flex align-items-center justify-content-between">
        <a href="#" class="header__brand" title="Logo">
            <img src="../assets/logo-png.png" alt="Logo">
        </a>
        <!-- Settings -->
        <div class="header__settings d-flex align-items-center">
            <div class="header__settings--fonts">
                <h3 class="title">
                    {{ currentFontStyle }}
                    <img src="../assets/down.png">
                </h3>
                <div class="options">
                    <h3 class="serif" :class="{'active': currentFontStyleId == 1}" @click="changeFontStyle" data-id="1">Serif</h3>
                    <h3 class="sans" :class="{'active': currentFontStyleId == 2}" @click="changeFontStyle" data-id="2">Sans Serif</h3>
                    <h3 class="mono" :class="{'active': currentFontStyleId == 3}" @click="changeFontStyle" data-id="3">Monospace</h3>
                </div>
            </div>
            <!-- Theme Switch -->
            <div class="header__settings--themes d-flex align-items-center">
                <input type="checkbox" class="toggle" v-model="themeToggle" @click="changeTheme">
                <div class="theme-imgs" id="themeImg">
                    <img src="../assets/dark-mode.png" class="light">
                    <img src="../assets/light.png" class="dark">
                </div>
            </div>
        </div>
    </div>
 </header>
</template>

<script>
export default {
    data() {
        return {
            themeToggle: false,
            theme: 'light',
            currentFontStyle: 'Serif',
            currentFontStyleId: 1
        }
    },
    created() {
        this.getTheme();
        this.getFontStyle();
    },
    methods: {
        changeTheme() {
            let theme = 'light';

            if (this.theme == 'light') {
                document.body.classList.add('dark');
                localStorage.setItem('theme', 'dark');
                this.theme = 'dark';
            } else {
                document.body.classList.remove('dark');
                localStorage.setItem('theme', 'light');
                this.theme = 'light';
            }
        },
        getTheme() {
            let theme = localStorage.getItem('theme');

            if (theme == 'dark') {
                document.body.classList.add('dark');
                localStorage.setItem('theme', 'dark');
                this.theme = 'dark';
                this.themeToggle = true;
            } else {
                document.body.classList.remove('dark');
                localStorage.setItem('theme', 'light');
                this.theme = 'light';
            }
        },
        changeFontStyle(e) {
            let id = e.target.getAttribute('data-id');
            this.currentFontStyleId = id;
            localStorage.setItem('fontStyleId', id);

            if (id == '1') {
                this.currentFontStyle = 'Serif';
                document.body.classList.remove('sans','mono');
                document.body.classList.add('serif');
            } else if (id == '2') {
                this.currentFontStyle = 'Sans Serif';
                document.body.classList.remove('serif','mono');
                document.body.classList.add('sans');
            } else if (id == '3') {
                this.currentFontStyle = 'Monospace';
                document.body.classList.remove('sans','serif');
                document.body.classList.add('mono');
            }
        },
        getFontStyle() {
            let id = localStorage.getItem('fontStyleId');
            this.currentFontStyleId = id;

            if (id) {
                if (id == '1') {
                    this.currentFontStyle = 'Serif';
                    document.body.classList.remove('sans','mono');
                    document.body.classList.add('serif');
                } else if (id == '2') {
                    this.currentFontStyle = 'Sans Serif';
                    document.body.classList.remove('serif','mono');
                    document.body.classList.add('sans');
                } else if (id == '3') {
                    this.currentFontStyle = 'Monospace';
                    document.body.classList.remove('sans','serif');
                    document.body.classList.add('mono');
                }
            }

        }
    }
}
</script>

<style lang="scss" scoped>
@use '../scss/variables' as var;

/* Header */
.header {
    padding: 30px 0;

    &__brand img {
        width: 45px;
    }

    // Settings
    &__settings {
        // Fonts
        &--fonts {
            position: relative;
            margin-right: 40px;

            .title {
                font-size: var.$fs-txt-20;
                font-weight: 700;
                display: flex;
                justify-content: center;
                align-items: center;
                cursor: pointer;

                img {
                    width: 22px;
                    margin-left: 10px;
                }
            }

            .options {
                position: absolute;
                top: 100%;
                left: 0;
                padding: 20px 30px;
                background: var.$clr-white;
                border-radius: 7px;
                transition: 0.3s;
                opacity: 0;
                box-shadow: 0 10px 20px rgba(0,0,0,0.05);
                pointer-events: none;

                h3 {
                    font-weight: 400;
                    font-size: var.$fs-txt-20;
                    margin: 8px 0;
                    cursor: pointer;
                    color: var.$clr-txt-grey;

                    &.active {
                        color: var.$clr-txt-dark;
                        font-weight: var.$fw-bold;
                    }

                    &.serif {
                        font-family: 'PT Serif', serif;
                    }
                    &.sans {
                        font-family: Inter, sans-serif;
                    }
                    &.mono {
                        font-family: 'Source Code Pro', monospace;
                    }
                }
            }
            
            .title:hover + .options, .options:hover {
                opacity: 1;
                pointer-events: all;
            }
        }

        /* Theme Switch */
        &--themes .theme-imgs {
            img {
                width: 36px;
                margin-left: 25px;

                &.dark {
                    display: none;
                }
            }
        }
    }
}

/* Toggle */
.toggle {
    position: relative;
    width: 40px;
    height: 20px;
    cursor: pointer;

    &::before {
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background: var.$clr-txt-grey;
        border-radius: 20px;
        transition: 0.3s;
    }

    &::after {
        content: '';
        position: absolute;
        left: 3px;
        top: 3px;
        width: 14px;
        height: 14px;
        border-radius: 50%;
        background: var.$clr-white;
        transition: 0.3s;
    }

    &:checked {
        &::before {
            background: var.$clr-white;
        }
        &::after {
            left: calc(100% - 16px);
            background: var.$clr-txt-grey;
        }
    }
}

// Dark Theme
body.dark {
    .header {
        &__brand {
            filter: invert(1);
        }

        &__settings {
            &--themes img {
                &.dark {
                    display: inline-block;
                    filter: invert(1);
                }
                &.light {
                    display: none;
                }
            }

            &--fonts {
                .title {
                    color: var.$clr-white;
                }

                .options {
                    background: var.$clr-bg-dark;

                    h3 {
                        opacity: 0.7;
                        color: var.$clr-lt-grey;

                        &.active {
                            opacity: 1;
                        }
                    }
                }
            }
        }
    }
}
</style>