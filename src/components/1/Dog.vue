<template>
  <span>Dog {{world}}</span>
</template>


<script>
export default {
  data() {
    return {
      world: "임시 세계"
    };
  },
  created() {
    console.log("Dog this.$parent", this.$parent);
    // 여기도 function() 익명함수의 this는 $parent를 가르키게 된다
    //상위 컴포넌트에 이벤트핸들러를 등록하여 해당 이벤트를 처리한다.
    this.$parent.$on("setWorldText", text => {
      this.world = text;
    });
  },
  methods: {}
};
</script>

<!-- 
<script lang="ts">
import { Component, Vue } from "vue-property-decorator";



export default class Dog extends Vue {
  world = "임시 세계";

  created() {
    console.log("Dog this.$parent", this.$parent);
    // 여기도 function() 익명함수의 this는 $parent를 가르키게 된다
    //상위 컴포넌트에 이벤트핸들러를 등록하여 해당 이벤트를 처리한다.
    //this.$parent.$on("setWorldText", (text: string) => {
    //  this.world = text;
    //});
  }
}
</script>
-->