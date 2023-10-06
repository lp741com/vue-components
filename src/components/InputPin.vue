<template>
  <ul>
    <li
      v-for="(number, index) in digits"
      :key="index"
      @click="setFocusOn(0)"
      :class="{ focused: digitsFocus[index] }"
    >
      <span class="input-value">{{ number }}</span>
      <input
        class="invisible-input"
        type="text"
        :data-input-pin-id="`digit-input-${index}`"
        @keydown="setDigitAt($event, index)"
        inputmode="numeric"
      />
    </li>
  </ul>
</template>
<script lang="ts" setup>
  import { onMounted, ref } from 'vue'

  const props = defineProps({
    numberOfDigits: {
      type: Number,
      default: 6,
    },
    modelValue: {
      type: String,
      default: '',
    },
    borderColor: {
      type: String,
      default: '#000',
    },
    focusedBorderColor: {
      type: String,
      default: '#3B82F6',
    },
    bgColor: {
      type: String,
      default: '#FFFFFF',
    },
    color: {
      type: String,
      default: 'inherit',
    },
    radius: {
      type: String,
      default: '100%',
    },
    borderWidth: {
      type: String,
      default: '3px',
    },
  })

  const emit = defineEmits(['update:modelValue'])

  const digitsInput = ref<Array<HTMLInputElement | null>>(
    new Array(props.numberOfDigits),
  )
  const digitsFocus = ref<Array<boolean | null>>(
    new Array(props.numberOfDigits),
  )
  const digits = ref<Array<number | null>>(new Array(props.numberOfDigits))

  const disabled = ref<boolean>(false)

  const setDigitAt = (digit: KeyboardEvent, position: number) => {
    const value = Number(digit.key).valueOf()

    if (value >= 0 && value <= 9 && !disabled.value) {
      digits.value[position] = Number(digit.key)
      if (position < digitsFocus.value.length - 1) {
        setFocusOn(position + 1)
      }

      if (position === digitsInput.value.length - 1) {
        disabled.value = true
        setTimeout(() => {
          const output = digits.value.join('')
          reset()
          emit('update:modelValue', output)
          disabled.value = false
        }, 250)
      }
    }
  }

  const reset = () => {
    digitsFocus.value = new Array(props.numberOfDigits)
    digits.value = new Array(props.numberOfDigits)
    digitsInput.value.forEach((el) => {
      el!.blur()
      el!.value = ''
    })
    setFocusOn(-1)
  }

  const setFocusOn = (position: number) => {
    const tempArray = digitsFocus.value.map(() => false)

    if (position >= 0) {
      tempArray[position] = true
      digitsInput.value[position] && digitsInput.value[position]!.focus()
      digitsFocus.value = tempArray
    }
  }

  onMounted(() => {
    const inputElements: Array<HTMLInputElement | null> = []
    for (let index = 0; index < digitsInput.value.length; index++) {
      inputElements.push(
        document.querySelector(`[data-input-pin-id='digit-input-${index}']`),
      )
    }
    digitsInput.value = inputElements
  })
</script>
<style scoped>
  ul {
    display: flex;
    gap: 0.1rem;
    list-style: none;
    padding: 0;
    justify-content: space-between;
  }

  ul li {
    width: calc(100% / 6);
    padding-top: calc(100% / 6);
    position: relative;
  }

  ul li .input-value {
    background-color: v-bind(bgColor);
    border: v-bind(borderWidth) solid v-bind(borderColor);
    display: flex;
    outline: none;
    inset-inline: unset;
    border-radius: v-bind(radius);
    cursor: pointer;
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
  }

  ul li.focused .input-value {
    border-color: v-bind(focusedBorderColor);
  }

  .input-value {
    flex: 1;
    border-radius: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    font-family: 'Arial', sans-serif;
    font-size: 100%;
    color: v-bind(color);
  }

  .invisible-input {
    position: absolute;
    bottom: 0;
    right: 0;
    border-radius: 250px;
    opacity: 0;
    top: -0.25rem;
    left: -0.25rem;
    text-align: center;
  }

  @media screen and (min-width: 1024px) {
    ul {
      gap: 0.2rem;
    }

    .input-value {
      font-size: 2rem;
    }
  }
</style>
