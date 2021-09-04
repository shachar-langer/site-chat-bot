<template>
  <div class="grid place-items-center">
    <div class="flex flex-col w-full max-w-3xl">
      <Message
        v-for="(conversation, index) in messages"
        :key="index"
        :time="conversation.time"
        :avatar="conversation.avatar"
        :content="conversation.content"
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
  data () {
    const firstMessage = messages[0]
    firstMessage.time = this.getTime()
    return {
      messages: [firstMessage],
      step: 0
    }
  },
  methods: {
    getTime () {
      const date = new Date()
      return `${date.getHours()}:${date.getMinutes()}`
    },
    showNextStep () {
      // No more messages
      if (messages.length === this.step + 1) {
        return
      }

      this.step = this.step + 1
      const nextMessage = messages[this.step]
      nextMessage.time = this.getTime()
      this.messages.push(nextMessage)

      // Continue if message doesn't include an action
      if (!nextMessage.action) {
        this.showNextStep()
      }
    },
    showAnswer (text) {
      const message = {
        time: this.getTime(),
        content: {
          type: 'text',
          attributes: {
            text: 'hello world'
          }
        },
        isAnswer: true
      }
      this.messages.push(message)
    },
    onYes () {
      this.showAnswer('Yes.')
      this.showNextStep()
    },
    onNo () {
      this.showAnswer('No.')
      console.log('Thank you very much for using my website')
    },
    onTextInput (textInput) {
      this.showAnswer(textInput)
      this.showNextStep()
    }
  }
}
</script>
