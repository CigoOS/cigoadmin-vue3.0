<template>
<div class="cigo-logo-area">
    <p class="short-title">{{Env.VUE_APP_SHORT_TAG}}</p>
    <p class="full-title">{{Env.VUE_APP_PROJECT_NAME_EN +" "+Env.VUE_APP_PROJECT_NAME_CN}}</p>
</div>
</template>

<script lang="ts">
import {
    defineComponent,
    onMounted,
    watch,
    ref,
    toRef,
    reactive
} from "vue";

import {
    systemStore
} from "@/store/index";
import {
    TweenMax
} from "gsap";

export default defineComponent({
    name: "LogoArea",
    setup() {
        let Env = reactive(process.env);
        let menuOpenFlag = toRef(
            systemStore.getState().systemState,
            "sideMenuOpen"
        );
        watch(menuOpenFlag, (openFlag: boolean, preOpenFLag: boolean) => {
            menuChange(openFlag);
        });

        onMounted(() => {
            menuChange(menuOpenFlag.value);
        });

        const menuChange = (openFlag: boolean) => {
            /** 隐藏者立即执行，显示者延迟200ms，以便隐藏到一定程度才显示 */
            /** 因为显示周期长于隐藏周期 */
            TweenMax.to(".short-title", openFlag ? 0.5 : 0.8, {
                opacity: openFlag ? 0 : 1,
                delay: openFlag ? 0 : 0.2
            });
            TweenMax.to(".full-title", openFlag ? 0.8 : 0.5, {
                opacity: openFlag ? 1 : 0,
                width: openFlag ? "182px" : "0px",
                delay: openFlag ? 0.2 : 0
            });
        };

        return {
            Env
        }
    }
});
</script>

<style lang="scss">
.cigo-logo-area {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 10vh;
    background-color: #1a2419;
    position: relative;
    border-bottom: 2px solid #2d373b;

    .short-title {
        color: #fff;
        font-size: 2.5em;
        font-weight: 900;
        font-style: italic;
        position: absolute;
    }

    .full-title {
        font-size: 1.15em;
        font-style: italic;
        color: #fff;
        font-weight: 700;
        overflow: hidden;
        position: absolute;
        white-space: nowrap;
        overflow: hidden;
    }
}
</style>
