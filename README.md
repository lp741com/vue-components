# Vue 3 Components library

Set of useful components for Vue3

[Demo](https://main.d9w2jiey2s1bk.amplifyapp.com/)

## 1. InputPin

```vue

<script setup>
  import InputPin from 'lp741-vue-components';
</script>
<template>
  <InputPin
      numeberOfDigits="6"
      v-model="otp"
      border-color="#9CA3AF"
      focused-border-color="#FCD34D"
      border-width="4px"
      radius="12px"
      bg-color="#efefef"
  ></InputPin>
</template>

```

### Options:

```javascript
  numberOfDigits: {
    type: Number,
default:
    6
}
,
modelValue: {
    type: String,
default:
    ''
}
,
borderColor: {
    type: String,
default:
    '#000'
}
,
focusedBorderColor: {
    type: String,
default:
    '#3B82F6'
}
,
bgColor: {
    type: String,
default:
    '#FFFFFF'
}
,
color: {
    type: String,
default:
    'inherit'
}
,
radius: {
    type: String,
default:
    '100%'
}
,
borderWidth: {
    type: String,
default:
    '3px'
}
```
