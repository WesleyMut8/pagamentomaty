<template>
  <div id="app" class="bg-background-image h-screen w-screen bg-cover">
    <div id="header" class="w-80 mx-auto flex flex-1 justify-center flex-col items-center">
        <div class="image-container mt-0">
          <img src="./src/assets/logo.svg" alt="Logo MATY" class="logo-image">
        </div>

        <label for="themeSwitcherOne" class="relative inline-flex select-none items-center justify-center w-80 mt-14 mx-0 rounded-full py-3">
          <input type="checkbox" name="themeSwitcherOne" id="themeSwitcherOne" class="sr-only" >
          <span class="text-laranja flex px-3 items-center justify-center w-full rounded-lg py-2 bg-white text-sm font-secundaria">
            <p>Após pagar envie o comprovante no whatsapp!</p>
          </span>
        </label>
    </div>

    <div v-if="isChecked" class="pix">
      <div id="body" class="bg-laranja rounded-xl flex flex-col justify-center items-center w-80 mx-auto p-4">
      <span class="text-white flex gap-1 items-center justify-center mx-auto w-1/5 rounded-full mb-3 bg-laranja bg-opacity-80 text-base font-secundaria">
          <img src="./src/assets/Pix.svg" class="w-6"/>
          <p class="text-center">Pix</p>
      </span>
        <h2 class="text-white font-secundaria text-lg">Selecione a quantidade de convites</h2>
        <div id="formHowMuchPerson" class="flex mt-3 items-center">
          <button name="minus" class="bg-amareloespecificotocompreguica rounded-full flex items-center z-index-9" @click="decrementPersonPix">
            <span class="font-auxiliar-bold text-white pt-1 px-5 text-5xl flex items-center">-</span>
          </button>      
          <div id="howMuchPerson" class="flex flex-col relative items-center w-25 max-w-[60%]">
              <img src="./src/assets/Pandeiro.svg" alt="Juta" class="w-4/5 mb-4">
              <p id="numberOfPerson" class="text-white ml-2 flex absolute items-center font-principal justify-center h-full w-full bottom-1 text-6xl left-0" v-text="numberOfPersonPix"></p>
          </div>
          <button name="plus" class="bg-amareloespecificotocompreguica rounded-full flex items-center z-index-9" @click="incrementPersonPix">
            <span class="font-auxiliar-bold text-white pt-1 px-4 text-5xl flex items-center">+</span>
          </button>
        </div>
      </div>

      <div v-if="numberOfPersonPix > 0" id="footer" class="flex w-80 mt-32 justify-end mx-auto">
      <div id="checkoutPix" class="w-40 bg-laranja rounded-xl flex flex-col items-center justify-center" @click="copyToClipboard(pixCopiaeCola)">
        <h3 class="font-secundaria text-white">Pix Copia e cola</h3>
        <img src="./src/assets/CopyIcon.svg" alt="Símbolo de Copiar" class="w-1/3"> 
        <p class="font-secundaria text-white">Clique para Copiar</p>
      </div>
    </div>
    </div>
  </div>
</template>

<script>
import './src/assets/styles.css';


export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      isChecked: true,
      numberOfPersonPix: 0,
    };
  },
  computed: {
    pixCopiaeCola() {
      switch (this.numberOfPersonPix) {
        case 1:
          return '00020126330014BR.GOV.BCB.PIX011111173140654520400005303986540560.005802BR5922Mariana Almeida Santos6009SAO PAULO61080540900062160512MATY1CONVITE6304AFB4';
        case 2:
          return '00020126330014BR.GOV.BCB.PIX0111111731406545204000053039865406120.005802BR5922Mariana Almeida Santos6009SAO PAULO61080540900062170513MATY2CONVITES6304CE43';
        case 3:
          return '00020126330014BR.GOV.BCB.PIX0111111731406545204000053039865406180.005802BR5922Mariana Almeida Santos6009SAO PAULO61080540900062170513MATY3CONVITES6304E97B';
        default:
          return (''); // Defina um retorno para quando numberOfPersonPix for 0 ou outro valor não especificado
      }
    }
  },
  methods: {
    incrementPersonPix() {
      if (this.numberOfPersonPix === 3) {
        alert('Caso queira mais de 3 convites favor chamar no whatsapp para gerar uma nova chave!');
      } else {
        this.numberOfPersonPix += 1;
      }
    },
    decrementPersonPix() {
      if (this.numberOfPersonPix > 0) {
        this.numberOfPersonPix -= 1;
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
  background-position: center;   /* centraliza horizontalmente e verticalmente */
  background-repeat: no-repeat;  /* evita repetição da imagem */
  background-size: cover;        /* cobre toda a tela */
}


.font-principal {
  font-family: bobby-jones;
}

.font-auxiliar-bold {
  font-family: bobby-jones;
  font-weight: 900;
}

.font-secundaria {
  font-family: bobby-jones;
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
  position: absolute;
  top: -150px;
  width: 320px !important; /* Largura definida */
}

</style>
