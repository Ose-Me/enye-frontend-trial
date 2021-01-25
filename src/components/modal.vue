<template>
  <transition name="modal-fade">
    <div class="modal-backdrop">
      <div class="modal-content"
        role="dialog"
        aria-labelledby="modalTitle"
        aria-describedby="modalDescription"

      >
        <header
          class="modal-header px-5 py-2"
          id="modalTitle"
        >
          <slot name="header">
           <h1>Profile Details</h1> 

            <span
              class="btn-close"
              @click="close"
              aria-label="Close modal"
            >
              x
            </span>
          </slot>
        </header>
        <section
          class="modal-body pl-5"
          id="modalDescription"
        >
          <slot name="body">
            I'm the default body!
          </slot>
        </section>
       
      </div>
    </div>
  </transition>
</template>

<script >
  export default {
    name: 'modal',
    methods: {
      close() {
        this.$emit('close');
      },
    },
  };
</script>


<style>
  .modal-backdrop {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: rgba(0, 0, 0, 0.1);
    z-index: 100;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .modal-content {
    display: flex;
    flex-direction: column;
    background: #FFFFFF;
    box-shadow: 0px 0px 15px 5px rgba(70, 70, 71, 0.1);
    overflow-x: auto;
  }

 .modal-header h1{
      font-size: 1.3rem;
  }

  .modal-header {
      display: flex;
    border-bottom: 1px solid #eeeeee;
    color:#49A73D;
    justify-content: space-between;
    align-items: center;
  }

  .modal-body {
    position: relative;
    padding: 20px 10px;
  }

  .btn-close {
    border: none;
    font-size: 30px;
    cursor: pointer;
    font-weight: 500;
    color:#49A73D;
    background: transparent;
  }

</style>