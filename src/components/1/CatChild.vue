<template>
  <span>Cat Child {{world}}</span>
</template>

<script>
export default {
  data() {
    return {
      world: "xx"
    };
  },
  created() {
    console.log("Cat Child this.$parent", this.$parent);
    this.$parent.$parent.$on("setWorldText", text => {
      this.world = text;
    });
    //여기서 익명함수 function(){}으로 이벤트를 등록할 경우
    // this가 window를 가르키기 때문에 this를 사용하려면
    // let thisClass = this 와같은 방법으로 뷰컴포넌트 객체를 넘겨주어야함
    //상위 컴포넌트를 통해 이벤트를 발생시킨다.
    //let emmitEvent = () => {
    //  this.$parent.$emit("setWorldText", "world22");
    //};

    //setTimeout(emmitEvent, 1000);
  },
  methods: {}
};
</script>