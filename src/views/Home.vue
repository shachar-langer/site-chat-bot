<template>
  <div class="grid place-items-center">
    <div class="flex flex-col w-full max-w-3xl">
      <Message
        v-for="(conversation,index) in messages"
        :key="index"
        :time="conversation.time"
        :avatar="conversation.avatar"
        :text="conversation.text"
        :action="conversation.action"
        :isAnswer="conversation.isAnswer || false"
        @yes="onYes"
        @no="onNo"
        @text-input="onTextInput"
      />
    </div>
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
    showNextStep() {
      // No more messages
      if (messages.length === this.step + 1) {
        return
      }

      this.step = this.step + 1
      const nextMessage = messages[this.step]
      this.messages.push(nextMessage)

      // Continue if message doesn't include an action
      if (!nextMessage.action) {
        this.showNextStep()
      }
    },
    showAnswer(text) {
      const message = {
        time: '14:00',
        text,
        isAnswer: true
      }
      this.messages.push(message)
    },
    onYes() {
      this.showAnswer('Yes.')
      this.showNextStep()
    },
    onNo() {
      this.showAnswer('No.')
      console.log('Thank you very much for using my website')
    },
    onTextInput(textInput) {
      this.showAnswer(textInput)
      this.showNextStep()
    }
  }
}
</script>