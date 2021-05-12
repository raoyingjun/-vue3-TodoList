<template>
  <teleport to="body">
    <transition name="fade">
      <div class="alert-mask" v-show="modelValue" @click="cancel">
        <div class="alert bounce-in">
          <div class="alert-title">{{ title }}</div>
          <div class="alert-content">{{ content }}</div>
          <div class="alert-footer">
            <div class="alert-footer-cancel" @click="cancel">{{ cancelText }}</div>
            <div class="alert-footer-confirm" @click="confirm">{{ confirmText }}</div>
          </div>
        </div>
      </div>
    </transition>
  </teleport>
</template>

<script lang="ts">

import { defineComponent } from 'vue'

export default defineComponent({
  props: {
    modelValue: {
      type: Boolean,
      required: true
    },
    title: {
      type: String,
      default: '提示'
    },
    content: {
      type: String,
      default: '请问你确定关闭该对话框吗？你的操作将不会自动保存'
    },
    cancelText: {
      type: String,
      default: '取消'
    },
    confirmText: {
      type: String,
      default: '确定'
    }
  },
  emits: ['update:modelValue', 'confirm', 'cancel'],
  methods: {
    closeAlert () {
      this.$emit('update:modelValue', false)
    },
    confirm () {
      this.closeAlert()
      this.$emit('confirm')
    },
    cancel () {
      this.closeAlert()
      this.$emit('cancel')
    }
  }
})
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.fade-enter-active, .fade-leave-active {
  transition: all 200ms;
}

.fade-enter-from, .fade-leave-to {
  opacity: 0;
}

@keyframes bounceIn{
  from {
    transform: scale(0);
  }
  to {
    transform: scale(1);
  }
}

.bounce-in {
  animation: bounceIn 200ms;
}

.alert {
  &-mask {
    display: flex;
    justify-content: center;
    align-items: center;
    background: {
      color: rgba(0, 0, 0, .5);
    }
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    top: 0
  }

  width: 50%;
  background: {
    color: white
  };
  padding: 10px;

  &-title {
    text: {
      align: center;
    }
    font: {
      size: 20px
    }
  }

  &-content {
    text-align: center;
    padding: 10px;
  }

  &-footer {
    display: flex;
    justify-content: space-around;

    &-confirm {
      color: #0088ff;
      cursor: pointer;
    }

    &-cancel {
      color: #a2a2a2;
      cursor: pointer;
    }
  }
}
</style>
