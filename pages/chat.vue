<template>
  <div class="c-wrap">
    <div ref="block" class="c-chat">
      <message
        v-for="(m, i) in messages"
        :key="i"
        :name="m.name"
        :text="m.text"
        :owner="m.id === user.id"
      />
    </div>
    <div class="c-form">
      <chat-form />
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex'
import Message from '@/components/Message'
import ChatForm from '@/components/ChatForm'

export default {
  middleware: ['chat'],
  components: { Message, ChatForm },
  head () {
    return {
      title: `Комната ${this.user.room}`
    }
  },
  // eslint-disable-next-line vue/order-in-components
  computed: mapState(['user', 'messages']),
  // eslint-disable-next-line vue/order-in-components
  watch: {
    messages () {
      setTimeout(() => {
        this.$refs.block.scrollTop = this.$refs.block.scrollHeight
      })
    }
  }
}
</script>

<style scoped>

  .c-wrap {
    height: 100%;
    position: relative;
    overflow: hidden;
  }

  .c-form {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    padding: 1rem;
    height: 80px;
    background: #212121;
  }

  .c-chat {
    position: absolute;
    top: 0;
    right: 0;
    left: 0;
    bottom: 80px;
    padding: 1rem;
    overflow-y: auto;
  }

</style>
