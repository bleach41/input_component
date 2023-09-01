<script setup>
    import { ref, defineProps, defineEmits } from "vue"
    const emit = defineEmits(["onTagsChange"])
    let tags = ref([])
    let currentValue = ref("")
    function handlekeyDown(e) {
        // if (e.key === 'Enter' && currentValue.value !== '') {
        //     tags.value.push(currentValue.value)
        //     currentValue.value = ''
        // }
        if (e.key === 'Backspace' && currentValue.value === '') {
            tags.value.pop()
            // props.onTagsChange(tags.value)
            emit('onTagsChange', tags.value)
        }
    }
    const deleteTag = (tag) => {
        tags.value = tags.value.filter((item) => item !== tag)
        // props.onTagsChange(tags.value)
        emit('onTagsChange', tags.value)
    }
    function hanldeSubmmit() {
        if (currentValue.value !== '') {
            const exist = tags.value.some((item) => item === currentValue.value)
            if (!exist) {

                tags.value.push(currentValue.value)
                currentValue.value = ''
                // props.onTagsChange(tags.value)
                emit('onTagsChange', tags.value)
            }
        }

    }

</script>

<template>
    <div class="inputTag">
        <div class="tags">
            <div class="tag" v-for="(tag, index) in tags" :key="index">
                {{ tag }} <button @click="deleteTag(tag)">✖</button>

            </div>
        </div>
        <form class="form" @submit.prevent="hanldeSubmmit">
            <input class="input" type="text" v-model="currentValue" @keydown="handlekeyDown">
        </form>
    </div>
</template>

<style scoped>
    .inputTag {
        display: inline-flex;
        border: 2px solid;
        border-radius: 3px;

    }

    .tags {
        display: flex;
        gap: 3px;
        padding: 5px;
    }

    .tags .tag {
        background-color: #303232;
        align-items: center;
        display: flex;
        padding: 10px;
        border: 1px solid #ccc;
        gap: 10px;
        /* align-content: center; */
        border-radius: 15px;
    }

    .inputTag .input {
        height: 3em;
        font-size: medium;
        background-color: #242424;
        border: none;
        outline: none;
        padding: 0 5px;
    }

    .form {
        align-items: center;
        display: inline-flex;
    }

    .tag button {

        background-color: transparent;
        padding: 0 5px;
    }
</style>