<template>
  <li class="shopItem">
    <div class="cart-tab-1">
        <div class="cart-item-check">
            <a href="javascipt:;" class="item-check-btn" :class="{'check': good.checked}" @click="selectedProduct(good)">
                <svg class="icon icon-ok"><use xlink:href="#icon-ok"></use></svg>
            </a>
        </div>
        <div class="cart-item-pic">
            <img v-bind:src="good.productImage" :alt="good.productName">
        </div>
        <div class="cart-item-title">
            <div class="item-name" v-text="good.productName"></div>
        </div>
        <div class="item-include">
            <dl>
                <dt>赠送:</dt>
                <dd v-for="item in good.parts">{{item.partsName}}</dd>
            </dl>
        </div>
    </div>
    <div class="cart-tab-2">
      <div class="item-price">{{good.productPrice | formatMoney("元")}}</div>
    </div>
    <div class="cart-tab-3">
      <div class="item-quantity">
        <div class="select-self select-self-open">
          <div class="quentity">
            <a href="javascript:;" @click="changeMoney(good,-1)">-</a>
            <input type="text" v-model="good.productQuentity" disabled>
            <a href="javascript:;" @click="changeMoney(good, 1)">+</a>
          </div>
        </div>
        <div class="item-stock">有货</div>
      </div>
    </div>
    <div class="cart-tab-4">
      <div class="item-price-total">{{good.productPrice * good.productQuentity | formatMoney("元")}}</div>
    </div>
    <div class="cart-tab-5">
        <div class="cart-item-opration">
            <a href="javascript:;" class="item-edit-btn" @click.stop="delConfirm(good)">
                <svg class="icon icon-del"><use xlink:href="#icon-del"></use></svg>
            </a>
        </div>
    </div>
  </li>
</template>

<script>
  export default {
    props: {
      good: {
        type: Object,
        required: true
      }
    },
    filters: {
      formatMoney(val, unit) {
        return val + ' ' + unit;
      }
    },
    name: 'app',
    methods: {
      selectedProduct(good) {
        if (!good.checked) {
          this.$set(good, 'checked', true);
        } else {
          good.checked = !good.checked;
        }
        this.$emit('selectedItem', good);
      },
      changeMoney(good, count) {
        if (good.productQuentity >= 1) {
          good.productQuentity += count;
          if (!good.checked && good.checked) {
            this.$emit('selectedItem', good);
          }
        }
      },
      delConfirm(good) {
        this.$emit('delGood', good);
      }
    }
  };
</script>

<style>
</style>
