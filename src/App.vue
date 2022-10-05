<template>
  <div class="container">
    <div class="header">
      Добавление товара
    </div>
    <div class="formCard">
      <div class="nameCardInput">
        <p>Наименование товара</p>
        <input v-model="name" type="text" placeholder="Введите наименование товара" />
      </div>
      <div class="aboutCardInput">
        <p>Описание товара</p>
        <input v-model="about" type="text" placeholder="Введите описание товара" />
      </div>
      <div class="imgCardInput">
        <p>Ссылка на изображение товара</p>
        <input v-model="image" type="text" placeholder="Ввежите ссылку" />
      </div>
      <div class="priceCardInput">
        <p>Цена товара</p>
        <input @keydown.enter="addCard" v-model="price" type="text" placeholder="Ввежите цену" />
      </div>
      <div class="butt">
        <button @click="addCard" type="buttton">Добавить товар</button>
      </div>
      <div>

      </div>
    </div>

    <div class="blockCards">
      <div v-for="(c, index) in prodactCards" :key="index" class="productCard">
        <div class="imgCard">
          <img :src="c.img" />
        </div>
        <div class="nameCard">
          {{c.name}}
        </div>
        <div class="aboutCard">
          {{c.about}}
        </div>
        <div class="priceCard">
          {{c.price}}руб.
        </div>
        <button @click="removeCard(c)" class="buttDel" type="button">Удалить</button>
      </div>
    </div>

  </div>
</template>

<script>


export default {
  name: 'App',
  data() {
    return {
      image: "",
      name: "",
      about: "",
      price: "",
      prodactCards: []
    }

  },

  created() {
    const cardsData = localStorage.getItem("cards");
    if (cardsData) {
      this.prodactCards = JSON.parse(cardsData);
    }
  },

  methods: {
    addCard() {
      const newCard = {
        img: this.image,
        name: this.name,
        about: this.about,
        price: this.price,
      };

      this.prodactCards.unshift(newCard);
      localStorage.setItem("cards", JSON.stringify(this.prodactCards));
      this.image = "";
      this.name = "";
      this.about = "";
      this.price = "";
    },

    removeCard(card) {
      this.prodactCards = this.prodactCards.filter(t => t != card);
    }
  },





}
</script>




<style>
.header {
  grid-area: header;
  font-family: 'Source Sans Pro';
  font-style: normal;
  font-weight: 600;
  font-size: 28px;
  line-height: 35px;
  color: #3F3F3F;
}

.formCard {
  grid-area: formCard;
  width: 332px;
  height: 440px;
  background: #FFFEFB;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
}

.nameCardInput p {
  position: relative;
  width: 95px;
  height: 13px;


  font-family: 'Source Sans Pro';
  font-style: normal;
  font-weight: 400;
  font-size: 10px;
  line-height: 13px;
  letter-spacing: -0.02em;
  color: #49485E;
}

.nameCardInput input {
  position: relative;
  width: 284px;
  height: 36px;


  background: #FFFEFB;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
}

.aboutCardInput p {
  width: 74px;
  height: 13px;


  font-family: 'Source Sans Pro';
  font-style: normal;
  font-weight: 400;
  font-size: 10px;
  line-height: 13px;
  letter-spacing: -0.02em;
  color: #49485E;
}

.aboutCardInput input {
  width: 284px;
  height: 108px;

  background: #FFFEFB;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
}

.imgCardInput p {
  width: 134px;
  height: 13px;


  font-family: 'Source Sans Pro';
  font-style: normal;
  font-weight: 400;
  font-size: 10px;
  line-height: 13px;
  letter-spacing: -0.02em;
  color: #49485E;

}

.imgCardInput input {
  width: 284px;
  height: 36px;

  background: #FFFEFB;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
}

.priceCardInput p {

  width: 53px;
  height: 13px;

  font-family: 'Source Sans Pro';
  font-style: normal;
  font-weight: 400;
  font-size: 10px;
  line-height: 13px;


  letter-spacing: -0.02em;

  color: #49485E;

}

.priceCardInput input {
  width: 284px;
  height: 36px;

  background: #FFFEFB;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  margin-bottom: 20px;
}

.butt button {
  width: 284px;
  height: 36px;

  background: #EEEEEE;
  border-radius: 10px;
  cursor: pointer;
}







.blockCards {
  grid-area: blockCards;
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
}


.imgCard img {
  width: 322px;
  height: 200px;

  border-radius: 4px 4px 0px 0px;
  padding-bottom: 10px;
  margin-right: 10px;
}

.nameCard {
  width: 201px;
  height: 25px;

  font-family: 'Source Sans Pro';
  font-style: normal;
  font-weight: 600;
  font-size: 20px;
  line-height: 25px;

  color: #3F3F3F;
  padding-bottom: 10px;

}

.aboutCard {
  width: 300px;
  height: 80px;


  font-family: 'Source Sans Pro';
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 20px;

  color: #3F3F3F;
  padding-bottom: 10px;
  word-wrap: break-word;
}

.priceCard {
  width: 117px;
  height: 30px;

  font-family: 'Source Sans Pro';
  font-style: normal;
  font-weight: 600;
  font-size: 24px;
  line-height: 30px;

  color: #3F3F3F;
  padding-bottom: 10px;
}

.buttDel {
  position: relative;
  width: 84px;
  height: 26px;

  background: #EEEEEE;
  border-radius: 10px;
  margin-bottom: 10px;
  cursor: pointer;
}







.container {
  display: grid;
  grid-template-areas:
    'header header'
    'formCard blockCards';

  grid-template-columns: 332px 1fr;
}
</style>
