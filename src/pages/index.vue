<template>
<div class="page-index">
    <h1>我是首页面1</h1>
    <div>
        <a-button type="primary">Primary</a-button>
        <a-button>Default</a-button>
        <a-button type="dashed">Dashed</a-button>
        <a-button type="danger">Danger</a-button>
        <a-config-provider :auto-insert-space-in-button="false">
            <a-button type="primary">按钮</a-button>
        </a-config-provider>
        <a-button type="primary">按钮</a-button>
        <a-button type="link">Link</a-button>
    </div>
</div>
</template>

<script lang="ts">
import {
    defineComponent
} from "vue";

export default defineComponent({
    name: "PagesIndex",
    setup() {}
});
</script>

<style lang="scss">
.page-index {
    display: flex;
    flex: 1;
    flex-direction: column;
}
</style>
