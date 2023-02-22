<template>
    <slide enter="right"
        leave="right"
        @after-leave="$emit('close')"
        v-show="visible">
        <div class="box quick-view is-marginless"
            :class="{ 'with-bookmarks': bookmarks }">
            <a class="delete is-pulled-right"
                @click="visible = false"/>
            <slot/>
        </div>
    </slide>
</template>

<script>
import { mapGetters } from 'vuex';
import { Slide } from '@enso-ui/transitions';

export default {
    name: 'QuickView',

    components: { Slide },

    emits: ['close'],

    data: () => ({
        visible: true,
    }),

    emits: ['close'],

    computed: {
        ...mapGetters('preferences', ['bookmarks']),
    },
};
</script>

<style lang="scss">
@import '@enso-ui/themes/bulma/variables';
    .quick-view {
        border-radius: 0;
        position: fixed;
        top: $navbar-height;
        right: 0;
        bottom: 0;
        z-index: 5;
        flex: 1 1 0%;
        display: block;

        &.with-bookmarks {
            top: 82px;
        }

        @media screen and (min-width: 1280px) {
            width: 30%;
        }

        @media screen and (min-width: 1024px) and (max-width: 1279px) {
            width: 45%;
        }

        @media screen and (min-width: 768px) and (max-width: 1023px) {
            width: 66%;
        }

        @media screen and (max-width: 767px) {
            width: 100%;
        }

        transition: top 0.5s;
        -webkit-transition: top 0.5s;
    }
</style>
