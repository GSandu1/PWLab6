<template>
    <div :class="['drawer', { 'is-open': isOpen }]">
      <button @click="toggleDrawer">Toggle Drawer</button>
      <div class="drawer-content">
        <nav>
          <router-link to="/">Home</router-link>
          <router-link to="/likedvideos">Liked Videos</router-link>
        </nav>
        <label class="switch">
          <input type="checkbox" @change="$emit('toggle-theme')" :checked="isDarkTheme">
          <span class="slider round"></span>
        </label>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: "Drawer",
    props: {
      isOpen: Boolean,
      isDarkTheme: Boolean
    },
    methods: {
        toggleDrawer() {
          // eslint-disable-next-line
            console.log('Toggling drawer'); // Check if this logs when the button is clicked
            this.$emit('toggle-drawer');
        }
    },

  }
  </script>
  
  <style scoped>
  .drawer {
    position: fixed;
    left: 0;
    top: 0;
    width: 250px;
    height: 100%;
    background-color: var(--background-color);
    box-shadow: 2px 0 5px rgba(0,0,0,0.5);
    transform: translateX(-100%);
    transition: transform 0.3s ease;
    z-index: 999;
  }
  
  .drawer.is-open {
    transform: translateX(0);
  }
  
  .switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
}

.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  transition: .4s;
  border-radius: 34px;
}

.slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  transition: .4s;
  border-radius: 50%;
}

input:checked + .slider {
  background-color: #2196F3;
}

input:focus + .slider {
  box-shadow: 0 0 1px #2196F3;
}

input:checked + .slider:before {
  transform: translateX(26px);
}

.slider.round {
  border-radius: 34px;
}

.slider.round:before {
  border-radius: 50%;
}

  </style>
  