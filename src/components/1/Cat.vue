<template>
  <div>
    <span>Cat</span>
    <br>
    <span>Cat Food: {{ food}}</span>
    <br>
    <!-- <CatChild v-on:cry="feed" /> -->
    <!-- <CatChild @cry="feed" /> -->
    <CatChild :cat-crying2="catCrying2" />
  </div>
</template>

<script>
import CatChild from "./CatChild.vue";
export default {
  components: {
    CatChild
  },
  data() {
    return {
      food: "yy",
      catCrying2: "meow"
    };
  },
  created() {
    console.log("Cat created");
    this.$on("setFeed", text => {
      this.food = text;
    });
    console.log("Cat this.$parent", this.$parent);
    //여기서 익명함수 function(){}으로 이벤트를 등록할 경우
    // this가 window를 가르키기 때문에 this를 사용하려면
    // let thisClass = this 와같은 방법으로 뷰컴포넌트 객체를 넘겨주어야함
    //상위 컴포넌트를 통해 이벤트를 발생시킨다.
    let emmitEvent = () => {
      //$emit() - 특정 범위를 이벤트로 부모에게 전달
      this.$parent.$emit("setSoundOfCrying", "meow");
    };
    //emmitEvent();
    //$parent.$emit를 통해 자신의 상위 객체에 이벤트를 트리거시키고, World.vue에서 $parent.$on을 통해 이벤트를 핸들링합니다.
    //트리거 시점이 핸들링 메서드가 등록된 이후여야 하므로 타임아웃을 걸어줍니다. 결과는 아래와 같습니다.
    setTimeout(emmitEvent, 1000);
  },
  mounted() {
    this.catCrying2 = "mew";
    console.log("Cat mounted");
  },
  methods: {
    feed() {
      console.log("feed");
      this.$parent.$emit("setFeed", "dogGum");
    }
  }
};
</script>
<!-- 
<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

export default class Cat extends Vue {
  created() {
    console.log("this.$parent", this.$parent);
    //console.log("this.$store App", this.$store);
    //여기서 익명함수 function(){}으로 이벤트를 등록할 경우
    // this가 window를 가르키기 때문에 this를 사용하려면
    // let thisClass = this 와같은 방법으로 뷰컴포넌트 객체를 넘겨주어야함
    //상위 컴포넌트를 통해 이벤트를 발생시킨다.
    //console.log("this.$parent", this.$parent);
    //let emmitEvent = () => {
    //  this.$parent.$emit("setWorldText", "world");
    //};
    //
    //setTimeout(emmitEvent, 1000);
  }
}
</script>
-->