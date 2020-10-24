<template>
  <div class="wrapper-popup" :class="{'open-popup': isOpenPopup === true}" @click="closePopup">
    <div class="rule" @click.stop="">
      <h3>Luật chơi</h3>
      <p>B1: Bấm vào nút new game.</p>
      <p>B2: Nhập final score.</p>
      <p>B3: Roll score.</p>
      <p>- Roll tiếp thì điểm sẽ cộng vào curent score.</p>
      <p>- Nếu roll vào số 1 sẽ đổi người chơi vào reset current score về 0.</p>
      <p>B4: Hold score</p>
      <p>- Player nào có số điểm tổng lớn hơn điểm final score sẽ winner.</p>
      <button class="btn-confirm" @click="closePopup">Đã Hiểu</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'popup-rule',
  props: {
    isOpenPopup: {type: Boolean, default: false}
  },
  data () {
    return {

    }
  },
  methods: {
    closePopup: function () {
      this.$emit('handleClosePopup')
    }
  }
}
</script>

<style>
  .wrapper-popup {
    position: fixed;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    background: rgba(0, 0, 0, 0.4);
    opacity: 0;
    visibility: hidden;
    transition: all .3s ease;
  }
  .wrapper-popup.open-popup {
    opacity: 1;
    visibility: visible;
  }
  .rule {
    padding: 2rem;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%) scale(1.2);
    background: #fff;
    position: absolute;
    font-family: Arial, Helvetica, sans-serif;
    transition: all .3s ease;
  }
  .open-popup .rule {
    transform: translate(-50%, -50%) scale(1);
  }
  .rule h3 {
    margin-bottom: 1rem;
  }
  .btn-confirm {
    padding: 0.5rem 1rem;
    margin-top: 1rem;
    background: #e6e6e6;
    color: #000;
    border-radius: 0.5rem;
    border: 1px solid #e6e6e6;
    cursor: pointer;
    transition: all .3s ease;
  }
  .btn-confirm:hover {
    background: rgb(71, 180, 71);
    color: #fff;
  }
</style>
