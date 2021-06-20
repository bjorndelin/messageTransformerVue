<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <br>
    <textarea v-model="message" placeholder="Add text to reverse..."></textarea>
    <br>
    <button v-bind:class="postData" @click="postData">REVERSE</button>
    <br>
    <br>
    <div class="result green">{{resultHeader}}</div>
    <div class="green">{{ result }}</div>

    <div class="result red">{{errorHeader}}</div>
    <div class="red">{{ error }}</div>
  </div>
</template>

<script>
import axios from 'axios';
  export default {
    name: 'MessageTransformer',
    props: {
      msg: String
    },
    data () {
      return {
        message: '',
        resultHeader: '',
        result: '',
        errorHeader: '',
        error: '',
        messageTransformerUrl: process.env.VUE_APP_MESSAGE_TRANSFORMER_URL
      }
    },
    methods: {
      postData: function() {
        if (this.message.trim() === '') {
          this.errorHeader = '';
          this.error = '';
          this.resultHeader = '';
          this.result = '';
          return;
        } else if (this.message.trim().length > 1000) {
          this.errorHeader = 'ERROR';
          this.error = 'The message is too long!';
          this.resultHeader = '';
          this.result = '';
          return;
        }

        const postBody = { message: this.message.trim(), messageDataType: 'WORD_REVERSAL' };

        axios.post(this.messageTransformerUrl, postBody)
            .then(response => {
              this.resultHeader = 'RESULT';
              this.result = response.data.result;
              this.errorHeader = '';
              this.error = '';
            })
            .catch(() => {
              this.errorHeader = 'ERROR';
              this.error = 'An error occurred!';
              this.resultHeader = '';
              this.result = '';

            })
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.green {
  font-weight: bold;
  color: green;
}
.red {
  font-weight: bold;
  color: red;
}
.result {
  font-size: 30px;
}
</style>