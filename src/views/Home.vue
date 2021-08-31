<template>
  <div class="flex flex-col">
    <Message
      v-for="(conversation,index) in messages"
      :key="index"
      :time="conversation.time"
      :avatar="conversation.avatar"
      :text="conversation.text"
      :action="conversation.action"
      @yes="onYes"
      @no="onNo"
      @text-input="onTextInput"
    />
  </div>
</template>

<script>
import Message from '@/components/Message.vue'
import messages from '../data/test_convo.json'

export default {
  components: { Message },
  data() {
    return {
      messages: [messages[0]],
      step: 0
    }
  },
  methods: {
    showNextMessage() {
      // No more messages
      if (messages.length === this.step + 1) {
        return
      }

      this.step = this.step + 1
      const nextMessage = messages[this.step]
      this.messages.push(nextMessage)

      // Continue if message doesn't include an action
      if (!nextMessage.action) {
        this.showNextMessage()
      }
    },
    onYes() {
      this.showNextMessage()
    },
    onNo() {
      console.log('Thank you very much for using my website')
    },
    onTextInput(textInput) {
      console.log(`The user entered ${textInput}`)
      this.showNextMessage()
    }
  }
}
</script>