<template>
    <div class="toots-wrapper" @click="favourTwoot(twoot.id)">
        <div class="username-position">
            <h2>@{{ username }}</h2>
        </div>
        <div class="twoots-position">
            <h2>{{ twoot.message }}</h2>
        </div>
    </div>

</template>

<script>
    export default {
        name: 'MessageItems',
        props: {
            username: {
                type: String,
                required: true
            },
            twoot: {
                type: Object,
                required: true
            }
        },
        methods: {
            favourTwoot(id){

                this.$emit('favourite', id)
            }
        }
    }
</script>

<style>

    h2 {
        font-size: 13px;
    }

    .toots-wrapper {
        padding: 20px;
        width: 100%;
        background-color: rgb(248, 248, 248);
        border: 1px solid #DFE3E8;
        border-radius: 5px;
        box-sizing: border-box;
        cursor: pointer;
        transform: all 0.25s ease;
    }

    .toots-wrapper:hover {
        transform: scale(1.1, 1.1);
    }

    .username-position {
        font-weight: bold;
    }

</style>