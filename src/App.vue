<template>
  <div class="wrapper">
    <form class="form" @submit.prevent="onSubmit">
      <span class="h1">Общая информация</span>
      <div
        class="form__group"
        :class="{ 'form__group--error': $v.formResponses.surname.$error }"
      >
        <label class="form__label">Фамилия</label>
        <input
          class="form__input"
          v-model.trim="$v.formResponses.surname.$model"
        />
        <div
          class="error"
          v-if="
            !$v.formResponses.surname.required &&
            $v.formResponses.surname.$error
          "
        >
          Вы забыли указать Фамилию
        </div>
      </div>
      <div
        class="form__group"
        :class="{ 'form__group--error': $v.formResponses.name.$error }"
      >
        <label class="form__label">Имя</label>
        <input
          class="form__input"
          v-model.trim="$v.formResponses.name.$model"
        />
        <div
          class="error"
          v-if="!$v.formResponses.name.required && $v.formResponses.name.$error"
        >
          Вы забыли указать имя
        </div>
      </div>
      <div class="form__group">
        <label class="form__label">Отчество</label>
        <input class="form__input" v-model.trim="formResponses.patronymic" />
      </div>
      <div
        class="form__group"
        :class="{ 'form__group--error': $v.formResponses.birth.$error }"
      >
        <label class="form__label">Дата рождения</label>
        <input
          class="form__input"
          v-model.trim="$v.formResponses.birth.$model"
        />
        <div
          class="error"
          v-if="
            !$v.formResponses.birth.required && $v.formResponses.birth.$error
          "
        >
          Вы забыли указать дату рождения
        </div>
        <div
          class="error"
          v-if="
            $v.formResponses.birth.required && !$v.formResponses.birth.checkDate
          "
        >
          Проверьте формат даты (ДД/ММ/ГГГГ)
        </div>
      </div>
      <div
        class="form__group"
        :class="{ 'form__group--error': $v.formResponses.phone.$error }"
      >
        <label class="form__label">Номер телефона</label>
        <input
          class="form__input"
          v-model.trim="$v.formResponses.phone.$model"
        />
        <div
          class="error"
          v-if="
            $v.formResponses.phone.$error && !$v.formResponses.phone.required
          "
        >
          Вы забыли указать номер телефона
        </div>
        <div
          class="error"
          v-if="
            !$v.formResponses.phone.checkPhone &&
            $v.formResponses.phone.required
          "
        >
          Проверьте формат номера
        </div>
      </div>
      <div class="form__group">
        <label class="form__label" for="select">Пол</label>
        <div id="select" class="form__select">
          <div class="options-container">
            <div class="option">
              <input type="radio" class="radio" id="grade-a" name="category" />
              <label for="grade-a">
                <h3>Мужчина</h3>
              </label>
            </div>
            <div class="option">
              <input type="radio" class="radio" id="grade-b" name="category" />
              <label for="grade-b">
                <h3>Женщина</h3>
              </label>
            </div>
          </div>
          <div class="selected">
            <h3>Мужчина</h3>
          </div>
        </div>
      </div>
      <div
        class="form__group"
        :class="{ 'form__group--error': $v.formResponses.clientGroup.$error }"
      >
        <label class="form__label">Группа клиента</label>
        <select
          class="form_multiselect"
          multiple
          data-placeholder="Группа клиента"
          v-model.trim="$v.formResponses.clientGroup.$model"
        >
          <option value="0">ОМС</option>
          <option value="1">Проблемные</option>
          <option value="2">VIP</option>
        </select>
        <div
          class="error"
          v-if="
            !$v.formResponses.clientGroup.checkClientGroup &&
            $v.formResponses.clientGroup.$error
          "
        >
          Вы забыли выбрать группу
        </div>
      </div>
      <div class="form__group">
        <label class="form__label" for="select">Лечащий врач</label>
        <div id="select" class="form__select">
          <div class="options-container">
            <div class="option">
              <input type="radio" class="radio" id="grade-a" name="category" />
              <label for="grade-a">
                <h3>Иванов</h3>
              </label>
            </div>
            <div class="option">
              <input type="radio" class="radio" id="grade-b" name="category" />
              <label for="grade-b">
                <h3>Захаров</h3>
              </label>
            </div>
            <div class="option">
              <input type="radio" class="radio" id="grade-с" name="category" />
              <label for="grade-с">
                <h3>Чернышева</h3>
              </label>
            </div>
          </div>
          <div class="selected">
            <h3>Иванов</h3>
          </div>
        </div>
      </div>
      <span class="h1">Адрес</span>
      <div class="form__group">
        <label class="form__label">Индекс</label>
        <input class="form__input" v-model.trim="formResponses.address.zip" />
      </div>
      <div class="form__group">
        <label class="form__label">Страна</label>
        <input
          class="form__input"
          v-model.trim="formResponses.address.country"
        />
      </div>
      <div class="form__group">
        <label class="form__label">Область</label>
        <input
          class="form__input"
          v-model.trim="formResponses.address.district"
        />
      </div>
      <div
        class="form__group"
        :class="{ 'form__group--error': $v.formResponses.address.city.$error }"
      >
        <label class="form__label">Город</label>
        <input
          class="form__input"
          v-model.trim="$v.formResponses.address.city.$model"
        />
        <div
          class="error"
          v-if="
            !$v.formResponses.address.city.required &&
            $v.formResponses.address.city.$error
          "
        >
          Вы забыли указать Город
        </div>
      </div>
      <div class="form__group">
        <label class="form__label">Улица</label>
        <input
          class="form__input"
          v-model.trim="formResponses.address.street"
        />
      </div>
      <div class="form__group">
        <label class="form__label">Дом</label>
        <input class="form__input" v-model.trim="formResponses.address.house" />
      </div>
      <span class="h1">Документы</span>
      <div
        class="form__group"
        :class="{
          'form__group--error': $v.formResponses.document.documentType.$error,
        }"
      >
        <label class="form__label" for="select">Тип документа</label>
        <div id="select" class="form__select">
          <div class="options-container">
            <div class="option">
              <input type="radio" class="radio" id="grade-a" name="category" />
              <label for="grade-a">
                <h3>Паспорт</h3>
              </label>
            </div>
            <div class="option">
              <input type="radio" class="radio" id="grade-b" name="category" />
              <label for="grade-b">
                <h3>Свидетельство о рождении</h3>
              </label>
            </div>
            <div class="option">
              <input type="radio" class="radio" id="grade-с" name="category" />
              <label for="grade-с">
                <h3>Вод. удостоверение</h3>
              </label>
            </div>
          </div>
          <div class="selected">
            <h3>Документ</h3>
          </div>
        </div>
        <div
          class="error"
          v-if="
            !$v.formResponses.document.documentType.required &&
            $v.formResponses.document.documentType.$error
          "
        >
          Выберите тип документа
        </div>
      </div>
      <div class="form__group">
        <label class="form__label">Серия</label>
        <input
          class="form__input"
          v-model.trim="formResponses.document.serialNumber"
        />
      </div>
      <div class="form__group">
        <label class="form__label">Номер</label>
        <input
          class="form__input"
          v-model.trim="formResponses.document.documentNumber"
        />
      </div>
      <div class="form__group">
        <label class="form__label">Кем выдан</label>
        <input
          class="form__input"
          v-model.trim="formResponses.document.issuedBy"
        />
      </div>
      <div
        class="form__group"
        :class="{
          'form__group--error': $v.formResponses.document.issueDate.$error,
        }"
      >
        <label class="form__label">Дата выдачи</label>
        <input
          class="form__input"
          v-model.trim="$v.formResponses.document.issueDate.$model"
        />
        <div
          class="error"
          v-if="
            !$v.formResponses.document.issueDate.required &&
            $v.formResponses.document.issueDate.$error
          "
        >
          Вы забыли указать дату выдачи документа
        </div>
        <div
          class="error"
          v-if="
            $v.formResponses.document.issueDate.required &&
            !$v.formResponses.document.issueDate.checkDate
          "
        >
          Проверьте формат даты (ДД/ММ/ГГГГ)
        </div>
      </div>
      <button
        class="button"
        type="submit"
        :disabled="submitStatus === 'PENDING'"
      >
        Создать
      </button>
      <p class="typo__p" v-if="submitStatus === 'OK'">Клиент создан</p>
      <p
        class="typo__p"
        :class="{ 'typo__p--error': submitStatus === 'ERROR' }"
        v-if="submitStatus === 'ERROR'"
      >
        Пожалуйста, проверьте введеные данные!
      </p>
      <p class="typo__p" v-if="submitStatus === 'PENDING'">Отправка...</p>
    </form>
    <div class="status__icon">
      <div v-if="submitStatus === 'OK'"></div>
    </div>
  </div>
</template>

<script>
import { required } from "vuelidate/lib/validators";
export default {
  data() {
    return {
      submitStatus: null,
      formResponses: {
        name: "",
        surname: null,
        phone: null,
        gender: "",
        birth: null,
        address: {
          city: null,
          street: null,
          zip: null,
          house: null,
          district: null,
          country: null,
        },
        document: {
          documentType: null,
          serialNumber: null,
          documentNumber: null,
          issuedBy: null,
          issueDate: null,
        },
        patronymic: null,
        clientGroup: [],
        attendingDoctor: null,
        sendSms: false,
      },
    };
  },
  mounted() {
    const selected = document.querySelectorAll(".selected");
    selected.forEach((el) =>
      el.addEventListener("click", () => {
        el.parentElement
          .querySelector(".options-container")
          .classList.toggle("active");
        el.parentElement.querySelectorAll(".option").forEach((option) => {
          option.addEventListener("click", () => {
            el.innerHTML = option.querySelector("label").innerHTML;
            if (
              el.closest(".form__group").querySelector(".form__label")
                .textContent === "Лечащий врач"
            ) {
              this.formResponses.attendingDoctor =
                option.querySelector("label").textContent;
            }
            if (
              el.closest(".form__group").querySelector(".form__label")
                .textContent === "Пол"
            ) {
              this.formResponses.gender =
                option.querySelector("label").textContent;
            }
            if (
              el.closest(".form__group").querySelector(".form__label")
                .textContent === "Тип документа"
            ) {
              this.formResponses.document.documentType =
                option.querySelector("label").textContent;
            }
            console.log(this.formResponses.gender);
            el.parentElement
              .querySelector(".options-container")
              .classList.remove("active");
          });
        });
      })
    );

    const select = document.querySelector("select[multiple]");
    const selectOptions = select.querySelectorAll("option");
    const newSelect = document.createElement("div");
    newSelect.classList.add("selectMultiple");
    const active = document.createElement("div");
    active.classList.add("active");
    const optionList = document.createElement("ul");
    const placeholder = select.dataset.placeholder;

    const span = document.createElement("span");
    span.innerText = placeholder;
    active.appendChild(span);

    selectOptions.forEach((option) => {
      let text = option.innerText;
      if (option.selected) {
        let tag = document.createElement("a");
        tag.dataset.value = option.value;
        tag.innerHTML = "<em>" + text + "</em><i></i>";
        active.appendChild(tag);
        span.classList.add("hide");
      } else {
        let item = document.createElement("li");
        item.dataset.value = option.value;
        item.innerHTML = text;
        optionList.appendChild(item);
      }
    });
    const arrow = document.createElement("div");
    arrow.classList.add("arrow");
    active.appendChild(arrow);

    newSelect.appendChild(active);
    newSelect.appendChild(optionList);

    select.parentElement.append(newSelect);
    span.appendChild(select);

    document
      .querySelector(".selectMultiple ul")
      .addEventListener("click", (e) => {
        let li = e.target.closest("li");
        if (!li) {
          return;
        }
        let select = li.closest(".selectMultiple");
        if (!select.classList.contains("clicked")) {
          select.classList.add("clicked");
          if (li.previousElementSibling) {
            li.previousElementSibling.classList.add("beforeRemove");
          }
          if (li.nextElementSibling) {
            li.nextElementSibling.classList.add("afterRemove");
          }
          li.classList.add("remove");
          let a = document.createElement("a");
          a.dataset.value = li.dataset.value;
          a.innerHTML = "<em>" + li.innerText + "</em><i></i>";
          a.classList.add("notShown");
          // a.style.display = "none";
          select.querySelector("div").appendChild(a); //might have to check later
          let selectEl = select.querySelector("select");
          let opt = selectEl.querySelector(
            'option[value="' + li.dataset.value + '"]'
          );
          opt.setAttribute("selected", "selected");
          setTimeout(() => {
            this.formResponses.clientGroup.push(li.dataset.value);
            a.classList.add("shown");
            select.querySelector("span").classList.add("hide");
          }, 300);
          //1st
          setTimeout(() => {
            let styles = window.getComputedStyle(li);
            let liHeight = styles.height;
            let liPadding = styles.padding;
            let removing = li.animate(
              [
                {
                  height: liHeight,
                  padding: liPadding,
                },
                {
                  height: "0px",
                  padding: "0px",
                },
              ],
              {
                duration: 300,
                easing: "ease-in-out",
              }
            );
            removing.onfinish = () => {
              if (li.previousElementSibling) {
                li.previousElementSibling.classList.remove("beforeRemove");
              }
              if (li.nextElementSibling) {
                li.nextElementSibling.classList.remove("afterRemove");
              }
              li.remove();
              select.classList.remove("clicked");
            };
          }, 300);
        }
      });

    document
      .querySelector(".selectMultiple > div")
      .addEventListener("click", (e) => {
        let a = e.target.closest("a");
        let select = e.target.closest(".selectMultiple");
        if (!a) {
          return;
        }
        a.className = "";
        a.classList.add("remove");
        select.classList.add("open");
        let selectEl = select.querySelector("select");
        let opt = selectEl.querySelector(
          'option[value="' + a.dataset.value + '"]'
        );
        let findedClientGroup = this.formResponses.clientGroup.indexOf(
          a.dataset.value
        );
        this.formResponses.clientGroup.splice(findedClientGroup, 1);
        opt.removeAttribute("selected");
        a.classList.add("disappear");
        setTimeout(() => {
          // start animation
          let styles = window.getComputedStyle(a);
          let padding = styles.padding;
          let deltaWidth = styles.width;
          let deltaHeight = styles.height;

          let removeOption = a.animate(
            [
              {
                width: deltaWidth,
                height: deltaHeight,
                padding: padding,
              },
              {
                width: "0px",
                height: "0px",
                padding: "0px",
              },
            ],
            {
              duration: 0,
              easing: "ease-in-out",
            }
          );

          let li = document.createElement("li");
          li.dataset.value = a.dataset.value;
          li.innerText = a.querySelector("em").innerText;
          li.classList.add("show");
          select.querySelector("ul").appendChild(li);
          setTimeout(() => {
            if (!selectEl.selectedOptions.length) {
              select.querySelector("span").classList.remove("hide");
            }
            li.className = "";
          }, 350);

          removeOption.onfinish = () => {
            a.remove();
          };
        }, 300);
      });
    document
      .querySelectorAll(
        ".selectMultiple > div .arrow, .selectMultiple > div span"
      )
      .forEach((el) => {
        el.addEventListener("click", () => {
          el.closest(".selectMultiple").classList.toggle("open");
        });
      });
  },
  validations: {
    formResponses: {
      surname: {
        required,
      },
      name: {
        required,
      },
      phone: {
        required,
        checkPhone(phone) {
          // eslint-disable-next-line no-useless-escape
          return /(?:7)[\d\-\(\) ]{9,}\d/g.test(phone);
        },
      },
      birth: {
        required,
        checkDate(birth) {
          return /^(?:(?:31(\/|-|\.)(?:0?[13578]|1[02]|(?:Jan|Mar|May|Jul|Aug|Oct|Dec)))\1|(?:(?:29|30)(\/|-|\.)(?:0?[1,3-9]|1[0-2]|(?:Jan|Mar|Apr|May|Jun|Jul|Aug|Sep|Oct|Nov|Dec))\2))(?:(?:1[6-9]|[2-9]\d)?\d{2})$|^(?:29(\/|-|\.)(?:0?2|(?:Feb))\3(?:(?:(?:1[6-9]|[2-9]\d)?(?:0[48]|[2468][048]|[13579][26])|(?:(?:16|[2468][048]|[3579][26])00))))$|^(?:0?[1-9]|1\d|2[0-8])(\/|-|\.)(?:(?:0?[1-9]|(?:Jan|Feb|Mar|Apr|May|Jun|Jul|Aug|Sep))|(?:1[0-2]|(?:Oct|Nov|Dec)))\4(?:(?:1[6-9]|[2-9]\d)?\d{2})$/gm.test(
            birth
          );
        },
      },
      address: {
        city: {
          required,
        },
      },
      clientGroup: {
        checkClientGroup(clientGroup) {
          return clientGroup.length !== 0;
        },
      },
      document: {
        documentType: {
          required,
        },
        issueDate: {
          required,
          checkDate(issueDate) {
            return /^(?:(?:31(\/|-|\.)(?:0?[13578]|1[02]|(?:Jan|Mar|May|Jul|Aug|Oct|Dec)))\1|(?:(?:29|30)(\/|-|\.)(?:0?[1,3-9]|1[0-2]|(?:Jan|Mar|Apr|May|Jun|Jul|Aug|Sep|Oct|Nov|Dec))\2))(?:(?:1[6-9]|[2-9]\d)?\d{2})$|^(?:29(\/|-|\.)(?:0?2|(?:Feb))\3(?:(?:(?:1[6-9]|[2-9]\d)?(?:0[48]|[2468][048]|[13579][26])|(?:(?:16|[2468][048]|[3579][26])00))))$|^(?:0?[1-9]|1\d|2[0-8])(\/|-|\.)(?:(?:0?[1-9]|(?:Jan|Feb|Mar|Apr|May|Jun|Jul|Aug|Sep))|(?:1[0-2]|(?:Oct|Nov|Dec)))\4(?:(?:1[6-9]|[2-9]\d)?\d{2})$/gm.test(
              issueDate
            );
          },
        },
      },
    },
  },
  methods: {
    onSubmit() {
      this.$v.$touch();
      if (this.$v.$invalid) {
        this.submitStatus = "ERROR";
      } else {
        // do your submit logic here
        this.submitStatus = "PENDING";
        setTimeout(() => {
          this.submitStatus = "OK";
        }, 500);
      }
    },
  },
};
</script>

<style lang="scss">
$error-color: #fc5a3e;
$textColor: #1e2330;
$primary: #dcdfe5;

* {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  box-sizing: border-box;
  padding: 0;
  margin: 0;
  font-size: 18px;
}
.wrapper {
  max-width: 1060px;
  display: flex;
  margin: 0 auto;
  @media only screen and(max-width:600px) {
    justify-content: center;
  }
}
.h1 {
  width: 100%;
  text-align: center;
  font-size: 26px;
  display: block;
  margin: 20px;
  font-weight: 500;
}
.form {
  // .form__group
  display: flex;
  flex-wrap: wrap;
  @media only screen and(max-width:600px) {
    min-width: 100%;
    justify-content: center;
    padding: 30px;
  }
  &__group {
    margin: 20px 0px;
    margin: 20px;
    min-width: calc(50% - 50px);
    display: flex;
    flex-direction: column;
    align-items: initial;
    justify-content: initial;
    @media only screen and(max-width:600px) {
      min-width: 100%;
    }
  }

  // .form__group--error

  &__group--error {
    color: $error-color;
    animation: shakeError 0.6s ease-in-out;
    & > input {
      border-color: #f79483;
      &:hover,
      &:focus {
        border-color: #f79483;
      }
    }
    & + .error {
      color: $error-color;
    }
  }

  // .form__label

  &__label {
    display: block;
    margin: 10px auto;
    width: 100%;
  }

  // .form__input

  &__input {
    font-size: 0.875rem;
    font-weight: 300;
    color: #374853;
    line-height: 2.375rem;
    min-height: 64px;
    position: relative;
    border: 1px solid #e8e8e8;
    border-radius: 5px;
    background: #fff;
    padding: 0 0.8125rem;
    width: 100%;
    transition: border 0.1s ease;
    box-sizing: border-box;
    outline: none;
    &:hover,
    &:focus {
      border-color: #b5b5b5;
    }
  }
}
.button {
  font-size: 0.875rem;
  font-weight: 500;
  color: #fff;
  min-height: 2.5rem;
  line-height: 1.4;
  padding: 0.5rem 1.875rem 0.625rem;
  box-sizing: border-box;
  position: relative;
  display: inline-block;
  background: #41b883;
  border: none;
  border-radius: 5px;
  z-index: 1;
  overflow: hidden;
  outline: none;
  vertical-align: middle;
  border-bottom: 3px solid #266d4d;
  text-decoration: none;
  transition: 0.1s;
  width: 100%;
  margin: 20px 30%;
  width: 100%;
  &:hover {
    background: #349268;
    cursor: pointer;
  }
  &:focus {
    outline: 0;
  }
}
.typo__p {
  width: 100%;
  margin: 20px;
  font-size: 23px;
  text-align: center;
  &--error {
    color: $error-color;
  }
}
.form__select {
  display: flex;
  flex-direction: column;
  position: relative;
  .options-container {
    max-height: 0;
    width: calc(100% - 12px);
    opacity: 0;
    transition: all 0.4s;
    overflow: hidden;
    border-radius: 5px;
    border: solid 1px #dcdfe5;
    background-color: #ffffff;
    order: 1;
    position: absolute;
    top: 68px;
    &::-webkit-scrollbar {
      width: 8px;
      background: #0d141f;
      background: #81878f;
      background: #f1f2f3;
      border-radius: 0 5px 5px 0;
    }
    &::-webkit-scrollbar-thumb {
      background: #525861;
      background: #81878f;
      border-radius: 0 5px 5px 0;
    }
  }
  label {
    h3 {
      font-family: "Open Sans", sans-serif;
      font-size: 14px;
      font-weight: 400;
      line-height: 1.57;
      color: #1f2949;
    }
    h5 {
      font-family: "Open Sans", sans-serif;
      font-size: 12px;
      font-weight: 400;
      line-height: 1.83;
      color: #81878f;
    }
    cursor: pointer;
  }
  .options-container.active {
    max-height: 240px;
    width: 100%;
    opacity: 1;
    overflow-y: scroll;
    z-index: 99;
    + {
      .selected {
        &::after {
          transform: translateY(-50%) rotateX(180deg);
        }
      }
    }
  }
  .option {
    padding: 12px 24px;
    cursor: pointer;
    &:hover {
      background: #dcdfe5;
    }
    .radio {
      display: none;
    }
  }
}
.selected {
  background: #2f3640;
  margin-bottom: 8px;
  position: relative;
  height: 64px;
  border-radius: 5px;
  border: solid 1px #dcdfe5;
  background-color: #ffffff;
  order: 0;
  padding: 12px 24px;
  cursor: pointer;
  display: flex;
  align-items: center;
  &::after {
    content: "\f078";
    font-family: "Font Awesome 5 Free";
    font-weight: 900;
    -webkit-font-smoothing: antialiased;
    display: inline-block;
    font-style: normal;
    font-variant: normal;
    text-rendering: auto;
    line-height: 1;
    position: absolute;
    right: 15px;
    top: 50%;
    transition: transform 0.5s;
    transform: translateY(-50%);
  }
  h3 {
    font-family: "Open Sans", sans-serif;
    font-size: 16px;
    font-weight: 400;
    line-height: 1.57;
    color: #1f2949;
  }
  h5 {
    font-family: "Open Sans", sans-serif;
    font-size: 12px;
    font-weight: 400;
    line-height: 1.83;
    color: #81878f;
  }
}
.selectMultiple {
  position: relative;
  select {
    display: none;
  }
  & > div {
    position: relative;
    height: 64px;
    display: flex;
    align-items: center;
    z-index: 2;
    padding: 8px 12px 2px 12px;
    border-radius: 8px;
    border: solid 1px #dcdfe5;
    background-color: #ffffff;
    font-size: 14px;
    min-height: 44px;
    transition: all 0.2s ease-in;
    cursor: pointer;
    .arrow {
      right: 1px;
      top: 0;
      bottom: 0;
      cursor: pointer;
      width: 28px;
      position: absolute;
      &:after {
        content: "";
        font-family: "Font Awesome 5 Free";
        font-weight: 900;
        -webkit-font-smoothing: antialiased;
        display: inline-block;
        font-style: normal;
        font-variant: normal;
        text-rendering: auto;
        line-height: 1;
        position: absolute;
        right: 15px;
        top: 50%;
        transition: transform 0.5s;
        transform: translateY(-50%);
      }
    }
    span {
      color: #99a3ba;
      display: block;
      position: absolute;
      left: 22px;
      cursor: pointer;
      top: calc(50% - 16px);
      line-height: 28px;
      transition: all 0.3s ease;
      &.hide {
        opacity: 0;
        visibility: hidden;
        transform: translate(-4px, 0);
      }
    }
    a {
      position: relative;
      padding: 0 24px 6px 8px;
      line-height: 28px;
      color: $textColor;
      display: inline-block;
      vertical-align: top;
      margin: 0 6px 0 0;
      em {
        font-style: normal;
        display: block;
        white-space: nowrap;
      }
      &:before {
        content: "";
        left: 0;
        top: 0;
        bottom: 6px;
        width: 100%;
        position: absolute;
        display: block;
        background: rgba(#e4e4e4, 0.7);
        z-index: -1;
        border-radius: 4px;
      }
      i {
        cursor: pointer;
        position: absolute;
        top: 0;
        right: 0;
        width: 24px;
        height: 28px;
        display: block;
        &:before,
        &:after {
          content: "";
          display: block;
          width: 2px;
          height: 10px;
          position: absolute;
          left: 50%;
          top: 50%;
          background: #000000;
          border-radius: 1px;
        }
        &:before {
          transform: translate(-50%, -50%) rotate(45deg);
        }
        &:after {
          transform: translate(-50%, -50%) rotate(-45deg);
        }
      }
      &.notShown {
        opacity: 0;
        transition: opacity 0.3s ease;
        &:before {
          width: 28px;
          transition: width 0.45s cubic-bezier(0.87, -0.41, 0.19, 1.44) 0.2s;
        }
        i {
          opacity: 0;
          transition: all 0.3s ease 0.3s;
        }
        em {
          opacity: 0;
          transform: translate(-6px, 0);
          transition: all 0.4s ease 0.3s;
        }
        &.shown {
          opacity: 1;
          &:before {
            width: 100%;
          }
          i {
            opacity: 1;
          }
          em {
            opacity: 1;
            transform: translate(0, 0);
          }
        }
      }
      &.remove {
        pointer-events: none;
        &:before {
          width: 28px;
          transition: width 0.4s cubic-bezier(0.87, -0.41, 0.19, 1.44) 0s;
        }
        i {
          opacity: 0;
          transition: all 0.3s ease 0s;
        }
        em {
          opacity: 0;
          transform: translate(-12px, 0);
          transition: all 0.4s ease 0s;
        }
        &.disappear {
          opacity: 0;
          transition: opacity 0.5s ease 0s;
        }
      }
    }
  }
  & > ul {
    margin: 0;
    padding: 0;
    list-style: none;
    font-size: 16px;
    z-index: 2;
    position: absolute;
    top: 100%;
    left: 0;
    right: 0;
    visibility: hidden;
    opacity: 0;
    border-radius: 8px;
    transform: translate(0, 20px) scale(0.8);
    transform-origin: 0 0;
    transition: all 0.4s ease,
      transform 0.4s cubic-bezier(0.87, -0.41, 0.19, 1.44),
      filter 0.3s ease 0.2s;
    li {
      // border: 1px solid black;
      color: $textColor;
      background: #fff;
      padding: 12px 16px;
      cursor: pointer;
      overflow: hidden;
      position: relative;
      transition: background 0.3s ease, color 0.3s ease,
        transform 0.3s ease 0.3s, opacity 0.5s ease 0.3s,
        border-radius 0.3s ease;
      &:first-child {
        border-radius: 8px 8px 0 0;
        &:last-child {
          border-radius: 8px;
        }
      }
      &:last-child {
        border-radius: 0 0 8px 8px;
        &:first-child {
          border-radius: 8px;
        }
      }
      &:hover {
        background: $primary;
        color: #fff;
      }
      &:after {
        content: "";
        position: absolute;
        top: 50%;
        left: 50%;
        width: 6px;
        height: 6px;
        background: rgba(#000, 0.4);
        opacity: 0;
        border-radius: 100%;
        transform: scale(1, 1) translate(-50%, -50%);
        transform-origin: 50% 50%;
      }
      &.beforeRemove {
        border-radius: 0 0 8px 8px;
        &:first-child {
          border-radius: 8px;
        }
      }
      &.afterRemove {
        border-radius: 8px 8px 0 0;
        &:last-child {
          border-radius: 8px;
        }
      }
      &.remove {
        transform: scale(0);
        opacity: 0;
        &:after {
          animation: ripple 0.4s ease-out;
        }
      }
      &.show {
        transform: scale(0);
        opacity: 0;
        animation: scale-up 0.35s ease forwards;
      }
    }
  }
  &.open {
    & > div {
      .arrow {
        &:after {
          transform: translateY(-50%) rotateX(180deg);
        }
      }
    }
    & > ul {
      transform: translate(0, 12px) scale(1);
      opacity: 1;
      visibility: visible;
    }
  }
}
.error {
  order: 3;
}
@keyframes ripple {
  0% {
    transform: scale(0, 0);
    opacity: 1;
  }
  25% {
    transform: scale(30, 30);
    opacity: 1;
  }
  100% {
    opacity: 0;
    transform: scale(50, 50);
  }
}
@keyframes scale-up {
  0% {
    transform: scale(0);
    opacity: 0;
  }
  100% {
    transform: scale(1);
    opacity: 1;
  }
}
@keyframes shakeError {
  0% {
    transform: translateX(0);
  }
  15% {
    transform: translateX(0.375rem);
  }
  30% {
    transform: translateX(-0.375rem);
  }
  45% {
    transform: translateX(0.375rem);
  }
  60% {
    transform: translateX(-0.375rem);
  }
  75% {
    transform: translateX(0.375rem);
  }
  90% {
    transform: translateX(-0.375rem);
  }
  100% {
    transform: translateX(0);
  }
}
</style>
