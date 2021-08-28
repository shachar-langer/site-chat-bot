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
            <div v-if="action.type==='input'">input</div>
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
            showAction: true
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
        }
    }
}
</script>
