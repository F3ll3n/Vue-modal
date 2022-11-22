<script>
export default {
  props: {
    show: Boolean,
  },
  data() {
    return {
        emailData: JSON.parse(localStorage.getItem('emails')) || [],
        emailsArr: '',
        email: '',
        message: '',
        isSubscribe: false,
        isAlreadySubscribed: false,
    }
  },
  methods: {
    setLocalItem(){
        // Функция добавления массива в localstorage и обновления состояния на странице.
        this.emailsArr = [...this.emailData, this.email];
        localStorage.setItem("emails", JSON.stringify(this.emailsArr));
        this.emailData = JSON.parse(localStorage.getItem('emails'))
    },
    submitForm(){
        // Условие проверяет, есть ли введённый email в массиве
        if(this.emailData.filter((item) => {return item == this.email}).length > 0){
            // Если email найден в массиве из локального хранилища, то ничего не делаем и выводим ошибку
            this.message = 'You have already subscribed to the newsletter';
            this.isAlreadySubscribed = true;
            this.isSubscribe = false;
        }
        else{
            // Если email не найден в массиве из локального хранилища, сохраняем его и выводим сообщение
            this.setLocalItem();
            this.message = 'You have successfully subscribed to the newsletter';
            this.isSubscribe = true;
            this.isAlreadySubscribed = false;
        }
    }
  }
}
</script>

<template>
  <Transition name="modal">
    <div v-if="show"  class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container">
            <div class="background-img"></div>
          <div class="modal-header">
            <p class="sale-font"><span class="weight-font">10%</span> off</p>
            <p class="sale-header-description">your first order</p>
            <div class="divider-block">
                <div class="divider">
            </div>
            <p class="sale-description">Subscrive to recieve 10% off promocode plus exclusive offers and deals</p>
            </div>
          </div>
          <div  class="modal-footer">
            <form @submit.prevent="submitForm()"  v-bind:class="{hidden: isSubscribe}" class="email-form" method="#">
                <label>
                    <p>Email-adress</p>
                    <input class="email-input" v-model="email" v-html="emailInput" required="required" type="email">
                </label>
                <button class="submit-button">
                    Subscribe!
                </button>
                <div class="radio">
                    <input required="required" type="checkbox" class="custom-checkbox custom-radio"  id="privacy">
                    <label for="privacy"><p>I’m agree with privacy policy</p></label>
                </div>
            </form>
            <p v-bind:class="{unsubscribeMessage: isAlreadySubscribed}" class="subscribe-message">{{message}}</p>
          </div>
          <div
            class="modal-default-button"
            @click="$emit('close')">
            <svg xmlns="http://www.w3.org/2000/svg" width="15" height="15" viewBox="0 0 15 15" fill="none"><path d="M13.6565 2.34326L2.34277 13.657M13.6565 13.657L2.34277 2.34326" stroke="#C24DFE" stroke-width="2" stroke-linecap="round"></path></svg>  
          </div>
          
        </div> 
      </div>
    </div>
  </Transition>
</template>

<style>
.modal-mask {
    font-family: 'Roboto', sans-serif;
    position: fixed;
    z-index: 9998;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: table;
    transition: opacity 0.3s ease;
    display: flex;
    justify-content: center;
    align-items: center;
}
.modal-wrapper{
    padding: 5%;
}
.modal-container {
    position: relative;
    z-index: 1;
    width: 800px;
    height: 422px;
    box-shadow: 0 8px 20px rgb(68 75 77 / 15%);
    border-radius: 8px;
    overflow: hidden;
    padding: 40px 32px;
    background-color: #fff;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
    transition: all 0.3s ease;
}
.background-img{
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    z-index: -2;
    background: url(../assets/background.jpg);
    background-repeat: no-repeat;
    background-position: right;
}
.modal-container p {
    padding: 0;
    margin: 0;
    color: #828688;
}
.modal-container .sale-font {
    color: #2F3639;
}
.modal-container .sale-header-description{
    padding: 5px 0 0 0;
}
.modal-container .modal-header .weight-font{
    font-size: 104px;
    line-height: 114px;
    padding: 0px;
    margin: 0px;
    color: #2F3639;
}
.modal-container .modal-header {
    max-width: 359px;
    font-size: 24px;
    font-weight: 700;
    padding: 0 0 40px 0;
    margin: 0 !important;
}
.modal-container .modal-header .sale-description{
    font-size: 14px;
    font-weight: 400;
    color: #595E61;
}
.divider{
    display: block;
    width: 67px;
    height: 2px;
    margin: 26px 0;
    background: #C24DFE;
    border-radius: 10px;
}
.email-form{
    opacity: 1;
    transition: 0.3s;
    display: flex;
    height: 150px;
    flex-direction: column;
    justify-content: space-between;
}
.email-form label p{
    color: #828688;
    font-size: 12px;
    font-weight: 700;
    padding: 0 0 8px 0;
}
.email-input{
    width: 302px;
    height: 40px;
    border: 1px solid #D5D7D7;
    border-radius: 6px;
    padding: 0 0 0 15px;
    outline: 0px;
    font-family: 'Roboto', sans-serif;
    box-sizing: border-box;
}
.modal-container .hidden{
    position: absolute;
    z-index: -9999;
    opacity: 0;
}
.email-input:focus{
    border: 2px solid #C24DFE;
    outline: 0px;
}

.submit-button{
    width: 106px;
    height: 40px;
    background-color: #C24DFE;
    border-radius: 35px;
    border: 0;
    font-weight: 700;
    font-size: 12px;
    cursor: pointer;
    color: #fff;
}
.radio label p{
    cursor: pointer;
    padding: 2px 12px 0 12px;
    font-size: 14px;
    color: #595E61;
    font-weight: 500;
}
.custom-radio {
    position: absolute;
    z-index: -1;
    opacity: 0;
}
.custom-radio+label {
    display: inline-flex;
    align-items: center;
    user-select: none;
}
.custom-radio+label::before {
    content: '';
    display: inline-block;
    width: 16px;
    height: 16px;
    border: 2px solid rgb(194, 77, 254);
    border-radius: 4px;
    box-sizing: border-box;
    background-repeat: no-repeat;
    background-position: center center;
    background-size: 50% 50%;
}
.custom-radio:focus+label::before {
    box-shadow: 0 0 0 3px rgba(194, 77, 254, 0.25);
}
.custom-radio:focus:not(:checked)+label::before {
  box-shadow: 0 0 0 3px rgba(194, 77, 254, 0.25);
}
.custom-radio+label::after{
    content: '';
    width: 8px;
    height: 8px;
    margin: 4px;
    border-radius: 2px;
    position: absolute;
    display: flex;
    opacity: 0;
    background-color: #C24DFE;
    transition: 0.2s;
}

.modal-container .subscribe-message{
    width: 300px;
    font-size: 20px;
    font-weight: 700;
    color: #00ba09;
}
.modal-container .unsubscribeMessage{
    font-size: 15px;
    color: #d60000;
    width: 345px
}
.custom-radio:checked+label::after{
    opacity: 1;
}
.custom-radio:checked+label::before {
    border-color: #C24DFE;
    background-color: #ffffff;
}
.custom-radio:disabled+label::before {
    background-color: #e9ecef;
}
.modal-enter-from {
    opacity: 0;
}
.modal-leave-to {
    opacity: 0;
}
.modal-enter-from .modal-container,
.modal-leave-to .modal-container {
    -webkit-transform: scale(1.1);
    transform: scale(1.1);
}
.modal-default-button{
    position: absolute;
    top: 0;
    padding: 12px 12px 0 0;
    right: 0;
    color: #000;
    cursor: pointer;
}
@media screen and (max-width: 988px) {
    .modal-container{
        max-width: 600px;
        width: 100%;
        height: 110%;
        box-sizing: border-box;
    }
    .modal-container .modal-header *{
        font-size: 18px;
    }
    .modal-container .modal-header .sale-font .weight-font{
        font-size: 60px;
    }
    .modal-container .modal-footer *{
        max-width: 600px;
        width: 100%;
    }
    .background-img{
        filter: opacity(15%);
        background-size: cover;
    }
    
}
</style>