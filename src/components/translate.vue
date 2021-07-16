<template>
  <div>
    <h2>Deepl translation API</h2>
    <form @submit.prevent="submitForm">
      <textarea
        name="originalText"
        required
        placeholder="Please enter the text you would like to translate"
        v-model="originalText"
      ></textarea>
      <select name="targetLanguage" required v-model="targetLanguage">
        <option value="" disabled selected>
          Please select the target language
        </option>
        <option value="BG">Bulgarian</option>
        <option value="CS">Czech</option>
        <option value="DA">Danish</option>
        <option value="DE">German</option>
        <option value="EL">Greek</option>
        <option value="EN">English</option>
        <option value="ES">Spanish</option>
        <option value="ET">Estonian</option>
        <option value="FI">Finnish</option>
        <option value="FR">French</option>
        <option value="HU">Hungarian</option>
        <option value="IT">Italian</option>
        <option value="JA">Japanese</option>
        <option value="LT">Lithuanian</option>
        <option value="LV">Latvian</option>
        <option value="NL">Dutch</option>
        <option value="PL">Polish</option>
        <option value="PT">Portuguese</option>
        <option value="RO">Romanian</option>
        <option value="RU">Russian</option>
        <option value="SK">Slovak</option>
        <option value="SL">Slovenian</option>
        <option value="SV">Swedish</option>
        <option value="ZH">Chinese</option>
      </select>
      <button type="submit">Submit</button>
    </form>

    <hr />
    <h2>Translation</h2>
    <p>{{ response }}</p>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "translate",
  data() {
    return {
      originalText: "",
      targetLanguage: "",
      response: "",
    };
  },
  methods: {
    submitForm() {
      axios
        .post("https://api-free.deepl.com/v2/translate", null, {
          params: {
            auth_key: "5652c0b9-adcf-7f2e-f6a2-3a577f700dc9:fx",
            text: this.originalText,
            target_lang: this.targetLanguage,
          },
        })
        .then((response) => {
          this.response = response.data.translations[0].text;
        })
        .catch((error) => {
          alert(error);
        });
    },
  },
};
</script>

