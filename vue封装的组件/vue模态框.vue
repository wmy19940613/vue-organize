<template>
    <transition name="confirm-fade">
        <div class="confirm" v-show="showFlag" @click.stop>
          <div class="confirm-wrapper">
              <div class="confirm-content">
                  <div>
                      <slot></slot>
                  </div>
                  <div class="operate">
                      <div @click="cancel" class="operate-btn left">{{cancelBtnText}}</div>
                      <div v-show="!singleChoice" @click="confirm" class="operate-btn right">{{confirmBtnText}}</div>
                  </div>
              </div>
          </div>
        </div>
    </transition>
</template>

<script type="text/ecmascript-6">
export default {
    props: {
        confirmBtnText: {
            type: String,
            default: '确定'
        },
        cancelBtnText: {
            type: String,
            default: '取消'
        },
        singleChoice: {
            type: Boolean,
            default: false
        }
    },
    data() {
        return {
            showFlag: false
        }
    },
    methods: {
        show() {
            this.showFlag = true
        },
        hide() {
            this.showFlag = false
        },
        cancel() {
            this.hide()
            this.$emit('cancel')
        },
        confirm() {
            this.hide()
            this.$emit('confirm')
        }
    }
}
</script>

<style scoped>
.confirm {
    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    z-index: 998;
    background-color: rgba(0, 0, 0, .3);
}

.confirm.confirm-fade-enter-active {
    animation: confirm-fadein 0.3s
}

.confirm.confirm-fade-enter-active .confirm-content {
    animation: confirm-zoom 0.3s
}

.confirm .confirm-wrapper {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    z-index: 999;
}

.confirm .confirm-wrapper .confirm-content {
    width: 290px;
    background: #fff;
    color: #5a5a5a;
    border-radius: 4px;
    overflow: hidden;
}

.confirm .confirm-wrapper .confirm-content .text {
    padding: 19px 15px;
    line-height: 22px;
    text-align: center;
    font-size: 16px;
}

.confirm .confirm-wrapper .confirm-content .operate {
    display: flex;
    align-items: center;
    text-align: center;
    font-size: 16px;
}

.confirm .confirm-wrapper .confirm-content .operate .operate-btn {
    flex: 1;
    line-height: 22px;
    padding: 8px 0;
    color: #5a5a5a;
}

.confirm .confirm-wrapper .confirm-content .operate .operate-btn.left {
    background: #f5f5f5;
}

.confirm .confirm-wrapper .confirm-content .operate .operate-btn.right {
    background: #00abf0;
    color: #fff;
}

@keyframes confirm-fadein {
    0% {
        opacity: 0
    }
    100% {
        opacity: 1
    }
}

@keyframes confirm-zoom {
    0% {
        transform: scale(0)
    }
    50% {
        transform: scale(1.1)
    }
    100% {
        transform: scale(1)
    }
}
</style>
