<template>
    <div class="mt-4">
        <div class="flex flex-row h-12 gap-1 items-end">
            <div class="text-xs">{{ time }}</div>
            <div class="w-12 h-12 relative">
                <div class="w-full h-full rounded-full overflow-hidden">
                    <img :src="avatar" alt="lovely avatar" />
                </div>
            </div>
            <div class="self-center rounded-full py-3 px-6 bg-purple-500 text-white">{{ text }}</div>
        </div>
        <div v-if="showAction" class="mt-2 ml-20">
            <div v-if="action.type==='yes-no'" class="flex flex-row gap-1">
                <button class="px-4 py-2 bg-purple-600 text-white rounded-xl" @click="onYes">Yes</button>
                <button class="px-4 py-2 bg-white text-purple-600 border-purple-600 border-2 rounded-xl" @click="onNo">No</button>
            </div>
            <div v-if="action.type==='text-input'">
                <div class="w-full max-w-sm">
                    <div class="flex items-center border-2 border-purple-500 py-2 rounded">
                        <input v-model="textInput" class="appearance-none bg-transparent border-none w-full text-gray-700 mx-2 py-1 px-2 leading-tight focus:outline-none" type="text" :placeholder="inputPlaceholder" :aria-label="inputLabel">
                        <button class="flex-shrink-0 bg-purple-500 hover:bg-purple-700 border-purple-500 hover:border-purple-700 text-sm border-4 text-white py-1 px-2 rounded mr-2" type="button" @click="onTextInputClick">
                            Save
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        time: {
            type: String,
            required: true
        },
        avatar: {
            type: String,
            required: true
        },
        text: {
            type: String,
            required: true
        },
        action: {
            type: Object,
            required: false,
            default: {}
        }
    },
    data() {
        return {
            showAction: this.action && Object.keys(this.action).length !== 0,
            textInput: ''
        }
    },
    methods: {
        onYes() {
            this.showAction = false
            this.$emit('yes')
        },
        onNo() {
            this.showAction = false
            this.$emit('no')
        },
        onTextInputClick() {
            this.showAction = false
            this.$emit('textInput', this.textInput)
        }
    },
    computed: {
        actionAttributes() {
            return (this.action && this.action.attributes) || {}
        },
        inputLabel() {
            return this.actionAttributes.inputLabel || 'Text Input'
        },
        inputPlaceholder() {
            return this.actionAttributes.placeholder || ''
        }
    }
}
</script>
