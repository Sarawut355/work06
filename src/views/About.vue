<template>
  <div class="about">
    <div class="text-danger">
      ****กรุณากดยืนยันเพื่อยืนยันสินค้าที่ท่านเลือก****
    </div>
    <div class="row">
      <product
        v-for="(item, index) in Menuitem"
        :key="index"
        :NameProduct="item.NameProduct"
        :img="item.img"
        :Price="item.Price"
        @Order="menuorder"
      />
    </div>
  </div>
</template>
<script>
import Product from "../components/Product.vue";
export default {
  components: { Product },
  props: {
    Menuitem: Array
  },
  data() {
    return {
      select: []
    };
  },
  methods: {
    menuorder(value) {
      this.select.push(value);
      this.$emit("Order", this.select);
    }
  }
};
</script>
<style></style>
