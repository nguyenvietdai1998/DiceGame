<template>
  <div class="wrapper-popup" v-bind:class="getClassPopup">
    <div class="rule">
      <h3>Luật chơi</h3>
      <p>
        Ngày 3/11, Cục Cảnh sát hình sự (CSHS) cho biết đã chủ trì phối hợp với
        các đơn vị nghiệp vụ Bộ Công an và công an địa phương triệt phá thành
        công đường dây đánh bạc do 2 đối tượng Đỗ Ngọc Hà (SN 1984, trú tại Long
        Biên, Hà Nội) và Bùi Hoàng Sơn (SN 1988, trú tại Cầu Giấy, Hà Nội) cầm
        đầu. Trong ảnh, chiếc Porsche biển khá đẹp có giá trị hàng tỷ đồng.
      </p>
      <button class="confirm" v-on:click="confirm">Đã hiểu</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "popup-rule",
  data() {
    return {};
  },

  props: {
    isOpenPopup: { type: Boolean, default: false },
  },

  methods: {
    confirm () {
      // Truyền thông tin cho thằng cha
      console.log('handleConfirm in Popup.vue');
      this.$emit('handleConfirm');
    },
  },

  computed: {
    getClassPopup: function () {
      return {
        "open-popup": this.isOpenPopup,
      };
    },
  },
};
</script>

<style>
.wrapper-popup {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgb(0, 0, 0, 0.4);
  opacity: 0;
  visibility: hidden;
}

.wrapper-popup.open-popup {
  opacity: 1;
  visibility: visible;
}

.rule {
  width: 350px;
  padding: 20px;
  font-family: Arial, Helvetica, sans-serif;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%) scale(1.2);
  background-color: #fff;
  position: absolute;
  transition: all 0.3s ease;
}

.open-popup .rule {
  transform: translate(-50%, -50%) scale(1);
}

.rule h3 {
  margin-bottom: 10px;
}
.rule .confirm {
  cursor: pointer;
  margin-top: 20px;
  padding: 8px 15px;
  border: 2px solid #333;
  background-color: #fff;
  transition: all 0.3s ease;
}

.rule .confirm:hover {
  color: #fff;
  background-color: #333;
}
/* kết hợp CSS3 với VueJs để xây dụng hiệu ứng - Zoom in - Zoom out */
</style>
