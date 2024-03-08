<template>
    <div v-if="isOpen" class="backdrop" @click="close">
      <div class="popup" @click.stop>
        <h1>Внимание!</h1>
        <hr />
        <slot></slot>
        <div class="footer">
          <slot name="actions" :confirm="confirm">
            <button class="glow-on-hover" @click="confirm">Подписаться</button>
          </slot>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      isOpen: {
        type: Boolean,
        required: true,
      },
    },
    emits: {
      ok: null,
      close: null,
    },
  
    methods: {
      confirm() {
        this.$emit("ok");
      },
    },
  };
  </script>
  
  <style>
  .popup {
    top: 50px;
    padding: 20px;
    left: 50%;
    transform: translateX(-50%);
    position: fixed;
    z-index: 101;
    background-color: #0332B3;
    border-radius: 10px;
    color: white;
  }
  
  .popup h1 {
    text-align: center;
    margin: 0;
  }
  
  .backdrop {
    position: fixed;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    background-color: rgba(0, 0, 0, 0.8);
    z-index: 100;
  }
  
  .footer {
    text-align: right;
  }
  button {
  margin: 0 auto;
  display: block;
} 


.glow-on-hover {
    width: 180px;
    height: 40px;
    border: none;
    outline: none;
    color: #f4f2f2;
    cursor: pointer;
    position: relative;
    z-index: 0;
    border-radius: 120px;
    font-size: 1rem;
}

.glow-on-hover:before {
    content: '';
    background: linear-gradient(45deg, #ff0000, #ff7300, #fffb00, #48ff00, #00ffd5, #002bff, #7a00ff, #ff00c8, #ff0000);
    position: absolute;
    top: -2px;
    left:-2px;
    background-size: 400%;
    z-index: -1;
    filter: blur(5px);
    width: calc(100% + 4px);
    height: calc(100% + 4px);
    animation: glowing 20s linear infinite;
    opacity: 0;
    transition: opacity .3s ease-in-out;
    border-radius: 10px;
    opacity: 1;
}

.glow-on-hover:active {
    color: #000
}

.glow-on-hover:active:after {
    background: transparent;
}


.glow-on-hover:after {
    z-index: -1;
    content: '';
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: #002bff;
    left: 0;
    top: 0;
    border-radius: 10px;
}

@keyframes glowing {
    0% { background-position: 0 0; }
    50% { background-position: 400% 0; }
    100% { background-position: 0 0; }
}

  </style>
  