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
                    Serif
                    <img src="../assets/down.png">
                </h3>
                <div class="options">
                    <h3 class="serif active">Serif</h3>
                    <h3 class="sans">Sans Serif</h3>
                    <h3 class="mono">Monospace</h3>
                </div>
            </div>
            <!-- Theme Switch -->
            <div class="header__settings--themes d-flex align-items-center">
                <input type="checkbox" class="toggle" v-model="darkTheme">
                <img src="../assets/dark-mode.png" class="theme-img">
            </div>
        </div>
    </div>
 </header>
</template>

<script>
export default {
    data() {
        return {
            darkTheme: false
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
                padding: 20px;
                background: var.$clr-white;
                border-radius: 7px;
                transition: 0.3s;
                opacity: 0;
                box-shadow: 0 10px 20px rgba(0,0,0,0.1);
                pointer-events: none;

                h3 {
                    font-weight: 400;
                    font-size: var.$fs-txt-20;
                    margin: 5px 0;
                    cursor: pointer;
                    color: var.$clr-txt-grey;

                    &.active {
                        color: var.$clr-txt-dark;
                        font-weight: 700;
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
        &--themes .theme-img {
            width: 36px;
            margin-left: 25px;
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
            left: calc(100% - 14px);
            background: var.$clr-txt-grey;
        }
    }
}
</style>