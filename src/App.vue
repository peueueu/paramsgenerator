<template>
  <div id="app">
    <MainTitle />
    <div class="container">
      <div class="input-controllers">
        <InputControl
          name="Old Site"
          @input="handleOldSite($event.target.value)"
        />
        <InputControl
          name="New Site"
          @input="handleNewSite($event.target.value)"
        />
      </div>
      <ButtonControl @click="genParams" />
    </div>

    <div class="code-wrapper">
      <transition name="fade">
        <div class="output-container" v-if="outputResponse">
          <pre>{{ outputResponse }}</pre>
        </div>
      </transition>
    </div>

    <notifications group="success" position="top left" />
    <notifications group="info" position="top center" />
  </div>
</template>

<script>
import MainTitle from "./components/MainTitle";
import InputControl from "./components/UI/InputControl";
import ButtonControl from "./components/UI/ButtonControl";

export default {
  name: "app",
  components: {
    MainTitle,
    InputControl,
    ButtonControl,
  },
  data() {
    return {
      oldSiteUrl: "",
      newSiteUrl: "",
      outputResponse: "",
    };
  },
  methods: {
    handleOldSite(value) {
      this.oldSiteUrl = value;
    },
    handleNewSite(value) {
      this.newSiteUrl = value;
    },
    genParams() {
      console.log(this.newSiteUrl, this.oldSiteUrl);
      if (this.oldSiteUrl && this.newSiteUrl) {
        this.outputResponse = `
        UPDATE wp_options SET option_value = replace(option_value, '${this.oldSiteUrl}','${this.newSiteUrl}') WHERE option_name = 'home' OR option_name = 'siteurl';
        UPDATE wp_posts SET guid = replace(guid, '${this.oldSiteUrl}','${this.newSiteUrl}');
        UPDATE wp_posts SET post_content = replace(post_content, '${this.oldSiteUrl}','${this.newSiteUrl}');
        UPDATE wp_postmeta SET meta_value = replace(meta_value,'${this.oldSiteUrl}','${this.newSiteUrl}');
        UPDATE wp_posts SET guid = REPLACE (guid, '${this.oldSiteUrl}', '${this.newSiteUrl}') WHERE post_type = 'attachment';
        `;
        this.$notify({
          group: "success",
          title: "E ainnnn manito 🐱‍👤",
          text: "Output Response generated with success!!! 😁😁",
        });
        // setTimeout(() => {
        //   this.outputResponse = "";
        // }, 10000);
      } else {
        this.$notify({
          group: "info",
          type: "warn",
          title: "Não vai dar não monstrão.",
          text: "Um ou mais inputs estão vazios. 😞",
        });
      }
    },
    // copyTestingCode() {
    //   let testingCodeToCopy = document.querySelector("#testing-code");
    //   testingCodeToCopy.setAttribute("type", "text"); // 不是 hidden 才能複製
    //   testingCodeToCopy.select();

    //   try {
    //     var successful = document.execCommand("copy");
    //     var msg = successful ? "successful" : "unsuccessful";
    //     alert("Testing code was copied " + msg);
    //   } catch (err) {
    //     alert("Oops, unable to copy");
    //   }
    // },
  },
};
</script>

<style lang="scss">
#app {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background: #345352;
}
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 400px;
  height: 300px;
  padding: 40px;
  background: #021c26;
  border-radius: 3px;
}

.code-wrapper {
  height: 200px;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.8s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active em versões anteriores a 2.1.8 */ {
  opacity: 0;
}

.output-container {
  padding: 50px;
}

.output-container pre {
  color: white;
  font-size: 1.25rem;
  line-height: 28px;
  font-weight: bold;
}
</style>
