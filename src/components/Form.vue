<template>
  <form autocomplete="off" class="form" @onsubmit="handleSubmit">
    <h2 class="form__title">Личные данные</h2>
    <div class="form__container">
      <div class="form__left-side">
        <div class="form__input">
          <CustomInput
            v-model="lastName"
            name="lastName"
            label="Фамилия"
            @input="handleInput"
          />
        </div>
        <div class="form__input">
          <CustomInput
            v-model="firstName"
            name="firstName"
            label="Имя"
            @input="handleInput"
          />
        </div>
        <div class="form__input">
          <CustomInput
            v-model="secondName"
            name="secondName"
            label="Отчество"
            @input="handleInput"
          />
        </div>
      </div>
      <div class="form__right-side">
        <div class="form__input">
          <CustomInput
            v-model="birthDate"
            name="birthDate"
            type="date"
            label="Дата рождения"
            placeholder="дд.мм.гггг"
            @input="handleInput"
          />
        </div>
        <div class="form__input">
          <CustomInput
            v-model="email"
            name="email"
            label="Email"
            @input="handleInput"
          />
        </div>
        <div class="form__input">
          <p class="form__label">Укажите ваш пол</p>
          <div class="form__radio-columns">
            <CustomRadioButton
              label="Мужской"
              name="sex"
              value="male"
              :is-checked="sex === 'male'"
              @change="handleInput"
            />
            <CustomRadioButton
              label="Женский"
              name="sex"
              value="female"
              :is-checked="sex === 'female'"
              @change="handleInput"
            />
          </div>
        </div>
      </div>
    </div>
    <h2 class="form__title">Паспортные данные</h2>
    <div class="form__container">
      <div class="form__input">
        <CustomSelect
          :options="citizenships"
          name="citizen"
          :maxItem="10"
          label="Гражданство"
          placeholder="Выберите гражданство"
          @selected="(item) => selectItem(item, 'citizen')"
        >
        </CustomSelect>
      </div>
    </div>
    <div v-if="showRussiaForm" class="form__container-three-column">
      <div class="form__input">
        <CustomInput
          v-model="passportSeries"
          name="passportSeries"
          label="Серия паспорта"
          @input="handleInput"
        />
      </div>
      <div class="form__input">
        <CustomInput
          v-model="passportNumber"
          name="passportNumber"
          label="Номер паспорта"
          @input="handleInput"
        />
      </div>
      <div class="form__input">
        <CustomInput
          v-model="passportDate"
          name="passportDate"
          type="date"
          label="Дата выдачи"
          placeholder="дд.мм.гггг"
          @input="handleInput"
        />
      </div>
    </div>
    <div v-else-if="showForeignForm">
      <div class="form__container">
        <div class="form__input">
          <CustomInput
            v-model="lastNameLatin"
            name="lastNameLatin"
            label="Фамилия на латинице"
            @input="handleInput"
          />
        </div>
        <div class="form__input">
          <CustomInput
            v-model="firstNameLatin"
            name="firstNameLatin"
            label="Имя на латинице"
            @input="handleInput"
          />
        </div>
      </div>
      <div class="form__container-three-column">
        <div class="form__input">
          <CustomInput
            v-model="passportNumber"
            name="passportNumber"
            label="Номер паспорта"
            @input="handleInput"
          />
        </div>
        <div class="form__input">
          <CustomSelect
            :options="citizenships"
            name="country"
            :maxItem="4"
            placeholder="Выберите страну выдачи"
            label="Страна выдачи"
            @selected="(item) => selectItem(item, 'country')"
          >
          </CustomSelect>
        </div>
        <div class="form__input">
          <CustomSelect
            :options="passportTypes"
            name="passportType"
            :maxItem="2"
            placeholder="Выберите тип паспорта"
            label="Тип паспорта"
            @selected="(item) => selectItem(item, 'passportType')"
          >
          </CustomSelect>
        </div>
      </div>
    </div>
    <div class="form__container">
      <div class="form__left-side">
        <div class="form__input">
          <p class="form__label">Меняли ли фамилию или имя?</p>
          <div class="form__radio-columns">
            <CustomRadioButton
              label="Да"
              name="changeName"
              value="1"
              :is-checked="changeName === '1'"
              @change="handleInput"
            />
            <CustomRadioButton
              label="Нет"
              name="changeName"
              value="0"
              :is-checked="changeName === '0'"
              @change="handleInput"
            />
          </div>
        </div>
      </div>
    </div>
    <div v-if="showChangeNameForm" class="form__container">
      <div class="form__input">
        <CustomInput
          v-model="lastNameChanged"
          name="lastNameChanged"
          label="Предыдущая фамилия"
          @input="handleInput"
        />
      </div>
      <div class="form__input">
        <CustomInput
          v-model="firstNameChanged"
          name="firstNameChanged"
          label="Предыдущее имя"
          @input="handleInput"
        />
      </div>
    </div>
    <footer class="form__footer">
      <CustomButton
        class="form__submit-button"
        type="submit"
        @click="handleSubmit"
      >
        Отправить
      </CustomButton>
    </footer>
  </form>
</template>

<script>
import CustomInput from "./CustomInput.vue";
import CustomRadioButton from "./CustomRadioButton.vue";
import CustomButton from "./CustomButton.vue";
import CustomSelect from "./CustomSelect";

export default {
  name: "Form",
  props: {
    citizenships: {
      type: Array,
      required: true,
      default: () => [],
    },
    passportTypes: {
      type: Array,
      required: true,
      default: () => [],
    },
  },
  components: {
    CustomSelect,
    CustomInput,
    CustomRadioButton,
    CustomButton,
  },
  data() {
    return {
      firstName: "",
      lastName: "",
      secondName: "",
      birthDate: "",
      email: "",
      sex: "male",
      citizen: "",
      country: "",
      passportSeries: "",
      passportNumber: "",
      passportDate: "",
      passportType: "",
      firstNameLatin: "",
      lastNameLatin: "",
      changeName: "0",
      lastNameChanged: "",
      firstNameChanged: "",
    };
  },
  computed: {
    showRussiaForm() {
      return this.citizen === "Russia";
    },
    showForeignForm() {
      return this.citizen && this.citizen.length > 0;
    },
    showChangeNameForm() {
      return this.changeName && this.changeName === "1";
    },
  },
  methods: {
    handleInput(event) {
      const { name, value } = event.target;
      this[name] = value;
    },
    selectItem(item, name) {
      switch (name) {
        case "citizen":
          this.citizen = item.name;
          break;
        case "country":
          this.country = item.name;
          break;
      }
    },
    handleSubmit(event) {
      event.preventDefault();
      console.log(JSON.stringify(this.$data));
      return false;
    },
  },
};
</script>

<style scoped>
.form {
  display: block;
  max-width: 1024px;
  min-height: 80vh;
  margin: 0 auto;
  padding: 24px 32px;
  background: #ffffff;
  box-shadow: 4px 4px 8px 0 rgba(34, 60, 80, 0.2);
}

.form__container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 0 16px;
}

.form__container-three-column {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 0 16px;
}

.form__title {
  margin: 0 0 24px;
}

.form__label {
  margin: 0 0 22px;
  font-size: 16px;
  line-height: 19px;
  color: rgba(34, 60, 80, 0.6);
}

.form__input {
  height: 71px;
  margin: 0 0 24px;
  box-sizing: border-box;
}

.form__radio-columns {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
}

.form__radio-columns > label:first-child {
  margin-right: 24px;
}

.form__footer {
  display: flex;
}

.form__submit-button {
  margin-left: auto;
}
</style>
