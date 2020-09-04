<template>
  <div class="code-wrapper">
    <transition name="fade">
      <div class="opacity-bg" v-if="show">
        <div class="wrapper-code">
          <div class="output-container">
            <!-- v-if="outputResponse" !-->
            <OutputArea :content="response" @click="copyTestingCode" id="testing-code" />
            <ButtonControl v-on="$listeners" class="close-btn" />
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
import ButtonControl from "./ButtonControl";
import OutputArea from "./OutputArea";
export default {
  components: {
    ButtonControl,
    OutputArea,
  },
  data() {
    return {
      isVisible: false,
    };
  },
  props: {
    response: {
      type: String,
    },
    show: {
      type: Boolean,
    },
  },
  methods: {
    copyTestingCode() {
      let testingCodeToCopy = document.querySelector("#testing-code");
      testingCodeToCopy.setAttribute("type", "text");
      testingCodeToCopy.select();

      try {
        var successful = document.execCommand("copy");
        var msg = successful ? "successful" : "unsuccessful";
        this.$notify({
          group: `${successful ? "success" : "error"}`,
          type: `${successful ? "success" : "error"}`,
          title: "Text Copied with Success. 🐱‍👤",
          text: `Code was copied ${msg}`,
        });
      } catch (err) {
        this.$notify({
          group: "error",
          type: "error",
          title: "Error on copying the code.",
          text: "Oops, unable to copy",
        });
      }

      testingCodeToCopy.setAttribute("type", "hidden");
      window.getSelection().removeAllRanges();
    },
  },
};
</script>

<style lang="scss">
.opacity-bg {
  width: 100%;
  height: 100vh;
  position: fixed;
  top: 0;
  left: 0;
  background: rgba(0, 0, 0, 0.3);
}

.wrapper-code {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.output-container {
  position: absolute;
  background: #fff;
  border-radius: 3px;
  padding: 40px 30px;

  .close-btn {
    background-repeat: no-repeat;
    top: -34px;
    right: -14px;
    color: tomato;
    position: absolute;
    height: 30px;
    background: url("../../assets/close.svg");
  }
}

.output-container pre {
  color: #1a1a1a;
  font-size: 0.75rem;
  line-height: 28px;
  font-weight: bold;
}
</style>
