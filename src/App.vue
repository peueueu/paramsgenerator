<template>
  <div id="app">
    <MainTitle title="Params Generator" />
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
      <ButtonControl @click="genParams" name="Generate Params" />
    </div>

    <OutputModal
      :response="outputResponse"
      :show="isVisible"
      @click="handleModalClose"
    />

    <notifications group="success" position="top left" />
    <notifications group="error" position="top right" />
    <notifications group="info" position="top center" />
  </div>
</template>

<script>
import MainTitle from "./components/MainTitle";
import InputControl from "./components/UI/InputControl";
import ButtonControl from "./components/UI/ButtonControl";
import OutputModal from "./components/UI/OutputModal";

export default {
  name: "app",
  components: {
    MainTitle,
    InputControl,
    ButtonControl,
    OutputModal,
  },
  data() {
    return {
      oldSiteUrl: "",
      newSiteUrl: "",
      outputResponse: "",
      isVisible: false,
    };
  },
  methods: {
    handleModalClose() {
      this.isVisible = false;
    },
    handleOldSite(value) {
      this.oldSiteUrl = value;
    },
    handleNewSite(value) {
      this.newSiteUrl = value;
    },
    genParams() {
      if (this.oldSiteUrl && this.newSiteUrl) {
        this.isVisible = true;
        this.outputResponse = `
        UPDATE wp_options SET option_value = replace(option_value, '${this.oldSiteUrl}','${this.newSiteUrl}')
        WHERE option_name = 'home' OR option_name = 'siteurl';
        UPDATE wp_posts SET guid = replace(guid, '${this.oldSiteUrl}','${this.newSiteUrl}');
        UPDATE wp_posts SET post_content = replace(post_content, '${this.oldSiteUrl}','${this.newSiteUrl}');
        UPDATE wp_postmeta SET meta_value = replace(meta_value,'${this.oldSiteUrl}','${this.newSiteUrl}');
        UPDATE wp_posts SET guid = REPLACE (guid, '${this.oldSiteUrl}', '${this.newSiteUrl}') WHERE post_type = 'attachment';
        `;
        this.$notify({
          group: "success",
          type: "success",
          title: "E ainnnn manito 🐱‍👤",
          text: "Output Response generated with success!!! 😁😁",
        });
      } else {
        this.$notify({
          group: "info",
          type: "warn",
          title: "Não vai dar não monstrão.",
          text: "Um ou mais inputs estão vazios. 😞",
        });
      }
    },
  },
};
</script>

<style lang="scss">
#app {
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background: linear-gradient(to bottom right, #003326, #003c3d);
}

// #app:before {
//   content: "";
//   position: absolute;
//   z-index: -1;
//   filter: hue-rotate(180deg);
//   background: url("./assets/main-bg.jpg");
//   width: 100%;
//   height: 100vh;
//   background-size: cotain;
// }

.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 400px;
  height: 300px;
  padding: 40px;
  background: #021c26;
  border-radius: 5px;
  box-shadow: 0px 10px 30px rgba(0, 0, 0, 0.5);
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
</style>
