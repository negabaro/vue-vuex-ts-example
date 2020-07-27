<template>
  <div>
    <button @click="clickOn">button </button>
    <br>
    <span>Cat Child {{catCrying2}}</span>
    <br>
    <span>Cat Child2: {{reversedMessage}}</span>
    <br>
    <span>Cat Child3: {{computedTestMessage}}</span>
    <br>
    <span>Cat Child4: {{methodTestMessage()}}</span>
    <br>
    <span>methods: {{methodCount}}</span>
    <br>
    <button @click="plusMethodCount"> + </button><button @click="minusMethodCount"> - </button>
    <br>
    <span>computed: {{computedCount}}</span>

  </div>

</template>

<script>
export default {
  //props: ["cat-crying2"],
  props: {
    catCrying2: {
      type: [String, Number], // String型に限定
      required: true, // 必須項目
      validator: function(value) {
        return ["meow", "mew"].indexOf(value) !== -1;
      }
    }
  },
  data() {
    return {
      methodCount: 0,
      computedCount: 0,
      computedTest: "test",
      catType: {
        type: "Russian Blue",
        sex: "female"
      }
      //cryingText: "mew"
    };
  },
  computed: {
    plusComputedCount() {
      this.computedCount++;
    },
    minusComputedCount() {
      this.computedCount--;
    },
    computedTestMessage() {
      console.log("computedTestMessage");
      return this.computedTest
        .split("")
        .reverse()
        .join("");
    },
    reversedMessage() {
      console.log("reversedMessage");
      return this.catCrying2
        .split("")
        .reverse()
        .join("");
    }
  },
  watch: {
    //catType() {
    //  console.warn("catType");
    //},
    catType: {
      handler() {
        console.warn("catType");
      },
      deep: true
    },
    catCrying2: {
      handler(val, oldVal) {
        console.warn(`catCrying2 handler oldValue: ${oldVal} value: ${val}`);
      },
      immediate: true
    }
    //catCrying2: "logMessage",
    //catCrying2: "logMessage2"
    //catCrying2(val, oldVal) {
    //  console.warn(`watched catCrying2 oldValue: ${oldVal} value: ${val}`);
    //}
    //cryingText() {
    //  console.warn("watch number");
    //}
  },
  created() {
    console.log("CatChild created");
    console.log("Cat Child this.$parent", this.$parent);
    this.$parent.$parent.$on("setSoundOfCrying", text => {
      //this.catCrying = text;
    });

    console.log("cry");
    this.$parent.$emit("cry", "ffuck");
    //여기서 익명함수 function(){}으로 이벤트를 등록할 경우
    // this가 window를 가르키기 때문에 this를 사용하려면
    // let thisClass = this 와같은 방법으로 뷰컴포넌트 객체를 넘겨주어야함
    //상위 컴포넌트를 통해 이벤트를 발생시킨다.
    //let emmitEvent = () => {
    //  this.$parent.$emit("setWorldText", "world22");
    //};

    //setTimeout(emmitEvent, 1000);

    //this.catType = null;
    this.catType.sex = "male";
    this.catType.type = "Bengal";
  },
  mounted() {
    console.log("CatChild mounted xxxx");
    //this.cryingText = "xxxx";
  },
  updated() {
    console.log("updated hook");
  },
  methods: {
    plusMethodCount() {
      this.methodCount++;
    },
    minusMethodCount() {
      this.methodCount--;
    },
    methodTestMessage() {
      console.log("methodTestMessage");
      return this.computedTest
        .split("")
        .reverse()
        .join("");
    },
    clickOn() {
      console.log("clickOn");
      this.computedTest = "lelesd";
      //this.computedTest = "test";
    },
    logMessage() {
      console.log("logMessage");
    },
    logMessage2(val, oldVal) {
      console.log(`logMessage2 oldValue: ${oldVal} value: ${val}`);
    }
  }
};
</script>