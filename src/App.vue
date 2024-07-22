<template>
  <div id="app" class="bg-background-image h-screen w-screen bg-cover">
    <div id="header" class="w-80 mx-auto flex flex-1 justify-center flex-col items-center">
        <div class="image-container mt-4">
          <img src="./assets/logo.svg" alt="Logo do Pagode do Negão 2.1" class="logo-image">
        </div>
        <label for="themeSwitcherOne" class="relative inline-flex select-none items-center justify-center gap-2 w-80 rounded-full p-3">
          <input type="checkbox" name="themeSwitcherOne" id="themeSwitcherOne" class="sr-only" v-model="isChecked">
          <span class="text-white flex px- items-center justify-center w-1/2 rounded-full py-2 bg-pink-600 text-lg font-secundaria isCheked:bg-pink-900">
              <p>Mudar para<span v-if="isChecked"> Cartão</span><span v-else> Pix</span></p>
          </span>
        </label>
    </div>

    <div v-if="isChecked" class="pix">
      <div id="body" class="bg-pink-600 rounded-xl flex flex-col justify-center items-center w-80 mx-auto p-4">
      <span class="text-white flex gap-1 items-center justify-center mx-auto w-1/5 rounded-full mb-3 bg-pink-600 bg-opacity-80 text-base font-secundaria">
          <img src="./assets/Pix.svg" class="w-6"/>
          <p class="text-center">Pix</p>
      </span>
        <h2 class="text-white font-secundaria text-xl">Selecione a quantidade de convites</h2>
        <div id="formHowMuchPerson" class="flex mt-4 items-center">
          <button name="minus" class="bg-white rounded-full flex items-center z-index-9" @click="decrementPersonPix">
            <span class="font-auxiliar-bold text-pink-600 pt-1 px-5 text-5xl flex items-center">-</span>
          </button>      
          <div id="howMuchPerson" class="flex flex-col relative items-center w-25 max-w-[60%]">
              <img src="./assets/Pandeiro.svg" alt="Pandeiro" class="w-3/5">
              <p id="numberOfPerson" class="text-pink-600 flex absolute items-center font-principal justify-center h-full w-full bottom-1 text-6xl left-0" v-text="numberOfPersonPix"></p>
          </div>
          <button name="plus" class="bg-white rounded-full flex items-center z-index-9" @click="incrementPersonPix">
            <span class="font-auxiliar-bold text-pink-600 pt-1 px-4 text-5xl flex items-center">+</span>
          </button>
        </div>
      </div>

      <div v-if="numberOfPersonPix > 0" id="footer" class="flex w-80 mt-32 justify-end mx-auto">
      <div id="checkoutPix" class="w-40 bg-pink-600 rounded-xl flex flex-col items-center justify-center" @click="copyToClipboard(pixCopiaeCola)">
        <h3 class="font-secundaria text-white">Pix Copia e cola</h3>
        <img src="./assets/CopyIcon.svg" alt="Símbolo de Copiar" class="w-1/3"> 
        <p class="font-secundaria text-white">Clique para Copiar</p>
      </div>
    </div>
    </div>

    <div v-else class="cartao">
      <div id="body" class="bg-pink-600 rounded-xl flex flex-col justify-center items-center w-80 mx-auto p-4">
        <span class="text-white flex gap-1 items-center justify-center mx-auto w-1/5 rounded-full mb-3 bg-pink-600 bg-opacity-80 text-base font-secundaria">
          <img src="./assets/CardIcon.svg" class="w-6"/>
          <p class="text-center">Cartão</p>
        </span>
        <h2 class="text-white font-secundaria text-xl">Selecione a quantidade de convites</h2>
        <div id="formHowMuchPerson" class="flex mt-4 items-center">
          <button name="minus" class="bg-white rounded-full flex items-center z-index-9" @click="decrementPersonCartao">
            <span class="font-auxiliar-bold text-pink-600 pt-1 px-5 text-5xl flex items-center">-</span>
          </button>      
          <div id="howMuchPerson" class="flex flex-col relative items-center w-25 max-w-[60%]">
              <img src="./assets/Pandeiro.svg" alt="Pandeiro" class="w-3/5">
              <p id="numberOfPerson" class="text-pink-600 flex absolute items-center font-principal justify-center h-full w-full bottom-1 text-6xl left-0" v-text="numberOfPersonCartao"></p>
          </div>
          <button name="plus" class="bg-white rounded-full flex items-center z-index-9" @click="incrementPersonCartao">
            <span class="font-auxiliar-bold text-pink-600 pt-1 px-4 text-5xl flex items-center">+</span>
          </button>
          </div>
      </div>

      <div v-if="numberOfPersonCartao > 0" id="footer" class="flex w-80 mt-32 justify-end mx-auto">
        <a id="checkoutPix" :href="linkPicpay" class="w-40 bg-pink-600 rounded-xl flex flex-col items-center justify-center">
          <h3 class="font-secundaria text-white">Link Picpay</h3>
          <img src="./assets/Picpay.svg" alt="Picpay" class="w-1/3"> 
          <p class="font-secundaria text-white">Clique para Acessar</p>
        </a>
      </div>
    </div>
  </div>
</template>

<script>
import './assets/styles.css';


export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      isChecked: true,
      numberOfPersonPix: 0,
      numberOfPersonCartao: 0,
    };
  },
  computed: {
    pixCopiaeCola() {
      switch (this.numberOfPersonPix) {
        case 1:
          return '00020126890014br.gov.bcb.pix013667a4e70a-22aa-49ed-8baa-68cd92fadfca0227Favor enviar o comprovante 520400005303986540550.005802BR5925Wesley Gabriel Neves Da C6009Sao Paulo62240520ConvitePagodedoNegao63046646';
        case 2:
          return '00020126890014br.gov.bcb.pix013667a4e70a-22aa-49ed-8baa-68cd92fadfca0227Favor enviar o comprovante 5204000053039865406100.005802BR5925Wesley Gabriel Neves Da C6009Sao Paulo62240520ConvitePagodedoNegao6304533F';
        case 3:
          return '00020126890014br.gov.bcb.pix013667a4e70a-22aa-49ed-8baa-68cd92fadfca0227Favor enviar o comprovante 5204000053039865406150.005802BR5925Wesley Gabriel Neves Da C6009Sao Paulo62240520ConvitePagodedoNegao63046A0C';
        case 4:
          return '00020126890014br.gov.bcb.pix013667a4e70a-22aa-49ed-8baa-68cd92fadfca0227Favor enviar o Comprovante 5204000053039865406200.005802BR5925Wesley Gabriel Neves Da C6009Sao Paulo62240520ConvitePagodedoNegao63045EE4';
        case 5:
          return '00020126890014br.gov.bcb.pix013667a4e70a-22aa-49ed-8baa-68cd92fadfca0227Favor enviar o Comprovante 5204000053039865406250.005802BR5925Wesley Gabriel Neves Da C6009Sao Paulo62240520ConvitePagodedoNegao630467D7';
        case 6:
          return '00020126880014br.gov.bcb.pix013667a4e70a-22aa-49ed-8baa-68cd92fadfca0226Favor enviar o Comprovante5204000053039865406300.005802BR5925Wesley Gabriel Neves Da C6009Sao Paulo62240520ConvitePagodedoNegao63046F0D';
        case 7:
          return '00020126890014br.gov.bcb.pix013667a4e70a-22aa-49ed-8baa-68cd92fadfca0227Favor enviar o comprovante 5204000053039865406350.005802BR5925Wesley Gabriel Neves Da C6009Sao Paulo62240520ConvitePagodedoNegao6304C777';
        case 8:
          return '00020126890014br.gov.bcb.pix013667a4e70a-22aa-49ed-8baa-68cd92fadfca0227Favor enviar o Comprovante 5204000053039865406400.005802BR5925Wesley Gabriel Neves Da C6009Sao Paulo62240520ConvitepagodedoNegao6304854A';
        case 9:
          return '00020126890014br.gov.bcb.pix013667a4e70a-22aa-49ed-8baa-68cd92fadfca0227Favor enviar o comprovante 5204000053039865406450.005802BR5925Wesley Gabriel Neves Da C6009Sao Paulo62240520ConvitePagodedoNegao6304FE76';
        case 10:
          return '00020126890014br.gov.bcb.pix013667a4e70a-22aa-49ed-8baa-68cd92fadfca0227Favor enviar o comprovante 5204000053039865406500.005802BR5925Wesley Gabriel Neves Da C6009Sao Paulo62240520ConvitePagodedoNegao630419E8';
        default:
          return (''); // Defina um retorno para quando numberOfPersonPix for 0 ou outro valor não especificado
      }
    },
    linkPicpay() {
      switch (this.numberOfPersonCartao) {
        case 1:
          return 'https://picpay.me/wesleyg27/50.0';
        case 2:
          return 'https://picpay.me/wesleyg27/100.0';
        case 3:
          return 'https://picpay.me/wesleyg27/150.0';
        case 4:
          return 'https://picpay.me/wesleyg27/200.0';
        case 5:
          return 'https://picpay.me/wesleyg27/250.0';
        case 6:
          return 'https://picpay.me/wesleyg27/300.0';
        case 7:
          return 'https://picpay.me/wesleyg27/350.0';
        case 8:
          return 'https://picpay.me/wesleyg27/400.0';
        case 9:
          return 'https://picpay.me/wesleyg27/450.0';
        case 10:
          return 'https://picpay.me/wesleyg27/500.0';
        default:
          return (''); // Defina um retorno para quando numberOfPersonCartao for 0 ou outro valor não especificado
      }
    },
  },
  methods: {
    incrementPersonPix() {
      if (this.numberOfPersonPix === 10) {
        alert('Caso queira mais de 10 convites favor chamar no whatsapp para gerar uma nova chave!');
      } else {
        this.numberOfPersonPix += 1;
      }
    },
    decrementPersonPix() {
      if (this.numberOfPersonPix > 0) {
        this.numberOfPersonPix -= 1;
      }
    },
    incrementPersonCartao() {
      if (this.numberOfPersonCartao === 10) {
        alert('Caso queira mais de 10 convites favor chamar no whatsapp para gerar um novo link!');
      } else {
        this.numberOfPersonCartao += 1;
      }
    },
    decrementPersonCartao() {
      if (this.numberOfPersonCartao > 0) {
        this.numberOfPersonCartao -= 1;
      }
    },
    copyToClipboard(value) {
      const el = document.createElement('textarea');
      el.value = value;
      el.setAttribute('readonly', '');
      el.style.position = 'absolute';
      el.style.left = '-9999px';
      document.body.appendChild(el);
      el.select();
      document.execCommand('copy');
      document.body.removeChild(el);
      alert('Chave pix Copia e Cola copiada com sucesso!');
    },
      redirectToPicpay() {
      window.location.href = this.linkPicpay;
    },
  }
}
</script>

<style>
.bg-background-image {
  background-image: url("~@/assets/Background.png");
}

.font-principal {
  font-family: dk;
}

.font-auxiliar-bold {
  font-family: bebas;
  font-weight: 900;
}

.font-secundaria {
  font-family: bebas;
}

.image-container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 120px; /* Altura definida */
    width: 100%; /* Preencha a largura disponível */
    overflow: hidden; /* Para garantir que nada ultrapasse o container */
}

.logo-image {
    width: 240px; /* Largura definida */
    height: 120px; /* Altura definida */
    object-fit: contain; /* Mantém a proporção da imagem */
}

</style>
