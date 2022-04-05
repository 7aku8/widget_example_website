<!-- Please remove this file from your project -->
<template>
  <div class="relative flex items-top justify-center min-h-screen bg-gray-100 sm:items-center sm:pt-0">
    <div id="widget_embed" />

    <div class="flex flex-col items-center gap-2">
      <h1 class="text-xl">Widget v2</h1>
      <span class="font-thin text-sm text-gray-500">Choose integration type to trigger widget's flow...</span>
      <div class="p-6 flex justify-center gap-6">
        <button @click="checkout" class="bg-white hover:bg-gray-100 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow">Checkout</button>
        <button @click="referral" class="bg-white hover:bg-gray-100 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow">Referral</button>
      </div>
      <div class="p-6 flex justify-center gap-6">
        <button @click="prod" class="bg-white hover:bg-gray-100 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow">Prod Miracle</button>
      </div>
    </div>
  </div>
</template>

<script>
// widget install !
import CryptoVoucherWidget from 'widget_embed_script';
// import 'widget_embed_script/dist/style.css';
import '../node_modules/widget_embed_script/dist/style.css'

function uuid() {
  const template = 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx';
  const xAndYOnly = /[xy]/g;

  return template.replace(xAndYOnly, (character) => {
    const randomNo = Math.floor(Math.random() * 16);
    const newValue = character === 'x' ? randomNo : (randomNo & 0x3) | 0x8;

    return newValue.toString(16);
  });
}

export default {
  name: 'Widget',
  methods: {
    checkout() {
      const widget = new CryptoVoucherWidget({
        selector: '#widget_embed',
        token: '2k2KCY7PC2u2J9uv9BeTe4yN',
        baseUrl: 'http://0.0.0.0:1234'
      });

      const uid = uuid()
      console.log('starting widget transaction | with uuid: ', uid)
      console.log('amount | ', 20)
      console.log('currency | ', 'EUR')
      widget.start(20, 'EUR', uid);
    },
    referral() {
      const widget = new CryptoVoucherWidget({
        selector: '#widget_embed',
        token: '2k2g257PC2u2J9uv9BeTe46U',
        baseUrl: 'https://widget-stage.cryptovoucher.io'
      });

      console.log('starting widget referral transaction')
      widget.start();
    },
    prod() {
      const widget = new CryptoVoucherWidget({
        selector: '#widget_embed',
        token: 'IxjnXrDUSftlHuAiFWovfsaN',
        baseUrl: 'https://widget-front.cryptovoucher.io'
      });

      console.log('starting widget referral transaction')
      widget.start(10, 'EUR', uuid());
    }
  }
}
</script>
