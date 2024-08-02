<template>
    <div class="formBlock-wrap">
      <form @submit.prevent="submitForm">
        <div class="left">
          <h2>ПРЕДСТАВТЕСЯ, БУДЬ ЛАСКА</h2>
          <label>
            * ПРІЗВИЩЕ
            <input type="text" v-model="form.lastName" required  :class="{ 'is-invalid': errors.lastName }"/>
            <span v-if="errors.lastName">{{ errors.lastName }}</span>
          </label>
          <label>
            * ІМ’Я
            <input type="text" v-model="form.firstName" required :class="{ 'is-invalid': errors.firstName }" />
            <span v-if="errors.firstName">{{ errors.firstName }}</span>
          </label>
          <label class="organization">
            ОРГАНІЗАЦІЯ ТА ПОСАДА
            <input type="text" v-model="form.organization" />
            <span v-if="errors.organization">{{ errors.organization }}</span>
          </label>
          <div class="roleBlock"> 
            <label class="role">
                <input type="radio" value="consumer" v-model="form.role" />
                СПОЖИВАЧ
            </label>
            <label class="role">
                <input type="radio" value="medical" v-model="form.role" />
                МЕДИЧНИЙ ПРАЦІВНИК
            </label>
            <label class="role">
                <input type="radio" value="journalist" v-model="form.role" />
                ЖУРНАЛІСТ
            </label>
        </div>
  
          <h2 class="message">ПОВІДОМЛЕННЯ</h2>
          <label>
            ТЕМА ПОВІДОМЛЕННЯ
            <input type="text" v-model="form.subject" />
            <span v-if="errors.subject">{{ errors.subject }}</span>
          </label>
          <label>
            * ПОВІДОМЛЕННЯ
            <textarea v-model="form.message" required :class="{ 'is-invalid': errors.message }"></textarea>
            <span v-if="errors.message">{{ errors.message }}</span>
          </label>
        </div>
        <div class="right">
           
          <h2>КОНТАКТНА ІНФОРМАЦІЯ</h2>
          <label>
            * EMAIL
            <input type="email" v-model="form.email" required  :class="{ 'is-invalid': errors.email }"/>
            <span v-if="errors.email">{{ errors.email }}</span>
          </label>
          <label>
            КРАЇНА
            <input type="text" v-model="form.country" />
            <span v-if="errors.country">{{ errors.country }}</span>
          </label>
          <label>
            МІСТО
            <input type="text" v-model="form.city" />
            <span v-if="errors.city">{{ errors.city }}</span>
          </label>
          <label>
            ІНДЕКС
            <input type="text" v-model="form.zip" />
            <span v-if="errors.zip">{{ errors.zip }}</span>
          </label>
          <label>
            АДРЕСА
            <input type="text" v-model="form.address" />
            <span v-if="errors.address">{{ errors.address }}</span>
          </label>
          <label>
            * ТЕЛЕФОН
            <input type="tel" v-model="form.phone" required :class="{ 'is-invalid': errors.phone }" placeholder="(___) ___-__-__" />
            <span v-if="errors.phone">{{ errors.phone }}</span>
          </label>
       
          <input type="submit" value="відправити" />
        </div>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    name: 'FormBlock',
    data() {
      return {
        form: this.getInitialForm(),
        errors: {}
      };
    },
    methods: {
      getInitialForm() {
        return {
          lastName: '',
          firstName: '',
          organization: '',
          role: '',
          subject: '',
          message: '',
          email: '',
          country: '',
          city: '',
          zip: '',
          address: '',
          phone: ''
        };
      },
      validateForm() {
        this.errors = {};
  
        const onlyCyrillic = /^[А-Яа-яЁёІіЇїЄєҐґ\s]+$/;
        const numbersOnly = /^[0-9]+$/;
        const addressPattern = /^[А-Яа-яЁёІіЇїЄєҐґ0-9\s\/\-\,]+$/;
        const alphanumericCyrillic = /^[А-Яа-яЁёІіЇїЄєҐґ0-9\s]+$/;
        const phonePattern = /^\+?[0-9]{7,15}$/;
  
        if (!onlyCyrillic.test(this.form.lastName)) {
          this.errors.lastName = 'Прізвище повинно містити тільки кирилицю';
        }
        if (!onlyCyrillic.test(this.form.firstName)) {
          this.errors.firstName = 'Ім’я повинно містити тільки кирилицю';
        }
        if (this.form.organization && !onlyCyrillic.test(this.form.organization)) {
          this.errors.organization = 'Організація та посада повинні містити тільки кирилицю';
        }
        if (this.form.country && !onlyCyrillic.test(this.form.country)) {
          this.errors.country = 'Країна повинна містити тільки кирилицю';
        }
        if (this.form.city && !onlyCyrillic.test(this.form.city)) {
          this.errors.city = 'Місто повинно містити тільки кирилицю';
        }
        if (this.form.subject && !alphanumericCyrillic.test(this.form.subject)) {
          this.errors.subject = 'Тема повідомлення повинна містити тільки цифри і кирилицю';
        }
        if (this.form.message && !alphanumericCyrillic.test(this.form.message)) {
          this.errors.message = 'Повідомлення повинно містити тільки цифри і кирилицю';
        }
        if (this.form.zip && !numbersOnly.test(this.form.zip)) {
          this.errors.zip = 'Індекс повинен містити тільки цифри';
        }
        if (this.form.address && !addressPattern.test(this.form.address)) {
          this.errors.address = 'Адреса повинна містити тільки цифри, кирилицю та символи "/", "-", ","';
        }
        if (!phonePattern.test(this.form.phone)) {
          this.errors.phone = 'Некоректний номер телефону';
        }
        if (!this.form.email) {
        this.errors.email = 'Email є обов’язковим';
      } else if (!this.validateEmail(this.form.email)) {
        this.errors.email = 'Email має бути коректним';
      }
  
        return Object.keys(this.errors).length === 0;
      },
      validateEmail(email) {
      const re = /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;
      return re.test(email);
    },
      submitForm() {
        if (this.validateForm()) {
          
          console.log('Форма відправлена', this.form);
          alert('Дані відправлені')
          this.form = this.getInitialForm();
        } else {
          console.log('Форма містить помилки', this.errors);
        }
      }
    }
  };
  </script>
  
  <style scoped>
  h2{
    margin-bottom: 52px;
    color: #000;

    font-size: 18px;
    font-style: normal;
    font-weight: 400;
    text-transform: uppercase;
  }
  .formBlock-wrap {
   display: flex;
   justify-content: center;
   align-items: center;
   width: 100%;
   margin-bottom: 79px;
   margin-top: 60px;

  }
  form{
    display: grid;
    grid-template-columns: 1fr 1fr;
    column-gap: 55px;
    width: fit-content;
  }
  input[type="text"],
  input[type="tel"],
  input[type="email"]{
    width: 246px;
    height: 35px;
    padding: 5px 12px;
  }

  label {
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: flex-start;
    margin-bottom: 10px;

    color: #000;

    font-family: Roboto;
    font-size: 12px;
    font-style: normal;
    font-weight: 400;
    text-transform: uppercase;
  }
.right label{
    margin-bottom: 17px;
}
.roleBlock {
    margin-top: 14px;
}
  textarea{
    height: 85px;
    width: 246px;

  }
  .message{
    margin-bottom: 18px;
    margin-top: 28px;
  }
  input[type="submit"]{
    width: 246px;
    background-color: #464646;
    stroke-width: 1px;
    stroke: #000;
    height: 31px;
    color: #FFF;
    margin-top: 56px;
    text-align: center;
    font-size: 22px;
    font-style: normal;
    font-weight: 400;
    text-transform: lowercase;
  }
  .organization{
    margin-top: 16px;
  }
  .role{
    width: 100%;
    display: flex;
    flex-direction: row;
    align-items: flex-start;
    justify-content: flex-start;
    gap: 11px;
  }

  .left,
  .right {
    /* display: flex;
    flex-direction: column;
    justify-content: space-between; */
    width: 255px;
  }

  span {
    color: red;
    font-size: 0.8em;
  }
  .is-invalid {
  border-color: red;
}
.is-invalid + span {
  color: red;
}

@media screen and (max-width: 579px) {
    form{
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: 1fr 1fr;
    row-gap: 55px;
    width: fit-content;
  }

}
  </style>
  