<template>
  <div class="nathanbate-dropdown-wrapper">
    <div @click="toggleShowing" v-click-away="onClickAway">
      <div class="nathanbate-dropdown-toggle-button-wrapper">
        <slot name="ToggleButton">
          <button>Toggle Button</button>
        </slot>
      </div>
      <transition name="dropdown-menu">
        <div class="nathanbate-dropdown" v-if="showing">
          <slot name="Dropdown">
            <div>
              <a href="https://google.com" target="_blank">
                Action Item 1
              </a>
            </div>
            <div>Action Item 2</div>
            <div>Action Item 3</div>
          </slot>
        </div>
      </transition>
    </div>
  </div>

</template>

<script>
import { directive } from 'vue3-click-away'

export default {
  name: 'DropdownMenu',
  directives: {
    ClickAway: directive
  },
  computed: {
    showing() {
      return this.menuState.showing
    },
  },
  data() {
    return {
      menuState: {
        showing: true,
      }
    }
  },
  methods: {
    toggleShowing() {
      this.menuState.showing = !this.menuState.showing
    },
    onClickAway() {
      this.menuState.showing = false
    }
  }

}
</script>

<style scoped>

  div.nathanbate-dropdown-wrapper {
    position: relative;
    display: flex;
    flex-direction: column;
    justify-items: right;
  }

  .nathanbate-dropdown-toggle-button-wrapper {
    display: flex;
    flex-direction: column;
    justify-items: right;
  }

 div.nathanbate-dropdown {
   position: absolute;
   transform-origin: top right;
   right: 0;
   margin-top: .5rem;
   background-color: white;
   /* border-radius: .5rem; */
   border: grey .01rem solid;
   padding-top: .5rem;
   padding-bottom: .5rem;
 }
 .dropdown-menu-enter-active,
 .dropdown-menu-leave-active {
   transition: all 0.2s;
 }
 .dropdown-content-enter,
 .dropdown-content-leave-to {
   opacity: 0;
   transform: translateY(-5px);
 }
</style>
