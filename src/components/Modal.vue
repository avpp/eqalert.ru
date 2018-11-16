<template>
  <transition name="modal">
    <div class="modal-mask">
      <div class="modal-wrapper" @click.self="$emit('close')">
        <div class="modal-container" :class="width_style">

          <div class="modal-header">
            <slot name="header">
              default header
            </slot>
            <button class="modal-header-close-button" @click.prevent="$emit('close')">×</button>
          </div>

          <div class="modal-body">
            <slot name="body">
              default body
            </slot>
          </div>

          <div class="modal-footer">
            <slot name="footer">
              default footer
              <button class="modal-default-button" @click="$emit('close')">
                OK
              </button>
            </slot>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
  export default {
    props: ['width'],
    computed: {
      width_style: function() {
        const styles = {'wide': 'modal-wide'}
        return styles[this.width || ''] || ''
      }
    }
  }
</script>

<style>
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, .5);
  display: table;
  transition: opacity .3s ease;
}

.modal-wrapper {
  vertical-align: middle;
  max-height: 100vh;
  overflow-y: scroll;
}

.modal-container {
  height: 100%;
  width: 300px;
  margin: 5vh auto;
  padding: 10px 15px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, .33);
  transition: all .3s ease;
  font-family: Helvetica, Arial, sans-serif;
}

.modal-container.modal-wide {
  width: 90% !important;
}

.modal-header h3 {
  margin-top: 0;
  color: #42b983;
}

.modal-body {
  margin: 10px 0;
}

.modal-default-button {
  float: right;
}
.modal-header-close-button {
  float: right;
  padding: 2px 0 0 0;
  cursor: pointer;
  font-size: 21px;
  font-wight: bold;
  color: black;
  opacity: 0.2;
  text-shadow: 0 1px 0 white;
  border: 0;
  background: transparent;
}
.modal-header-close-button:hover {
  opacity: 0.5;
}

/*
 * The following styles are auto-applied to elements with
 * transition="modal" when their visibility is toggled
 * by Vue.js.
 *
 * You can easily play with the modal transition by editing
 * these styles.
 */

.modal-enter {
  opacity: 0;
}

.modal-leave-active {
  opacity: 0;
}

.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
</style>
