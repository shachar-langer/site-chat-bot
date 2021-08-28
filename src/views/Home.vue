<template>
  <div class="flex flex-col">
    <Message v-for="(conversation,index) in messages" :key="index" :time="conversation.time" :avatar="conversation.avatar" :text="conversation.text" :action="conversation.action" @yes="onYes" @no="onNo"/>
  </div>
</template>

<script>
import Message from '@/components/Message.vue'
import conversations from '../data/test_convo.json'

export default {
  components: { Message },
  data() {
    return {
      messages: [conversations[0]],
      step: 0
    }
  },
  methods: {
    onYes() {
      this.step = this.step + 1
      this.messages.push(conversations[this.step])
    },
    onNo() {
      alert('Thank you very much for using my website')
    }
  }
}
</script>