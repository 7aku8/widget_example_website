<template>
  <div>
    <div id="widget_embed" />

    <div class="p-6 flex justify-center gap-4">
      <button @click="checkout">Checkout</button>
      <button @click="referral">Referral</button>
    </div>
    <Tutorial/>
  </div>
</template>

<script>
// widget install !
import CryptoVoucherWidget from 'widget_embed_script';
// import 'widget_embed_script/dist/style.css';
import '../node_modules/widget_embed_script/dist/style.css'

export default {
  name: 'IndexPage',
  methods: {
    checkout() {
      function uuid() {
        const template = 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx';
        const xAndYOnly = /[xy]/g;

        return template.replace(xAndYOnly, (character) => {
          const randomNo = Math.floor(Math.random() * 16);
          const newValue = character === 'x' ? randomNo : (randomNo & 0x3) | 0x8;

          return newValue.toString(16);
        });
      }

      const widget = new CryptoVoucherWidget({
        selector: '#widget_embed',
        token: '2k2KCY7PC2u2J9uv9BeTe4yN',
        baseUrl: 'https://widget-stage.cryptovoucher.io'
      });

      const uid = uuid()
      console.log('starting widget transaction | with uuid: ', uid)
      console.log('amount | ', 25)
      console.log('currency | ', 'EUR')
      widget.start(25, 'EUR', uid);
    },
    referral() {
      const widget = new CryptoVoucherWidget({
        selector: '#widget_embed',
        token: '2k2g257PC2u2J9uv9BeTe46U',
        baseUrl: 'https://widget-stage.cryptovoucher.io'
      });

      console.log('starting widget referral transaction')
      widget.start();
    }
  }
}
</script>
