<template>
  <!-- $attrs는 non-prop의 모든속성을 버튼에 넘겨준다 -->
  <button v-bind="$attrs" :type="type" :class="classes" ref="button">
    <!-- SLOT은 시작태그와 종료태그 사이에 들어가는 내용 -->
     <!-- 버튼에 들어갈 글자를 넣는다 -->
     <!-- <MyButton>My Button</MyButton> -->
    <slot></slot> 
    {{ classes }}
  </button>
  
</template>

<script>
import {ref, onMounted} from 'vue'

export default {
  props: {
    type: {
      default: 'button',
      validator: (value) => {
        const allowed = ['button', 'submit', 'reset', 'switch']
        return allowed.includes(value);
      },
    },

    sm: Boolean,
    md: {
      type: Boolean,
      default: true,
    },
    lg: Boolean,
    pill: Boolean,
  },

  setup(props, context) {
    const classes = ref([]);
    const button = ref(null);

    if(props.active=!'active'){
      classes.push('deactive')
    }
    if(props.sm) classes.push('sm');
    else if(props.lg) classes.push('lg');
    else classes.push('md');

    if (props.pill) classes.push('pill');

    onMounted( () => {
      // non-prop으로 처리되는 변수들
      Object.keys(context.attrs).forEach((attr) => {
        console.log(attr);
        if(attr.startsWith('text-')) {
          button.value.style.color= attr.substring(5)
        }
        if(attr.startsWith('background-')) {
          button.value.style.backgroundColor= attr.substring(11)
        }
      })
    })

    return {
      classes,
      button,
    }
  },
}
</script>

<style scoped>
button {
  outline: none;
}
.sm {
  height: 20px;
  font-size: 13px;
}
.md {
  height: 30px;
  font-size: 22px;
}
.lg {
  height: 40px;
  font-size: 31px;
}
.pill {
  border-radius: 16px;
}
</style>

