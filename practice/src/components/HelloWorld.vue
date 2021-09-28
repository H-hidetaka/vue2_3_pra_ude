<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <a :href="google">googleへのリンク</a>
    <hr>
    <br>
    <input v-bind="{name:formInput.name, placeholder:formInput.placeholder}">
    <input v-bind="formInput">
    <br>
    <div v-show="isDisplay">
      表示
    </div>
    <div v-show="!isDisplay">
      非表示
    </div>
    <br>
    <div v-if="isDisplay">
      ifで表示
    </div>

    <div v-if="signal === 'red'">赤</div>
    <div v-else-if="signal === 'yellow'">黄</div>
    <div v-else-if="signal === 'blue'">青</div>
    <div v-else>赤青黄ではない</div>

    <ul>
      <li v-for="member in members" :key="member.id">
        {{ member }}
      </li>
    </ul>


    <ul>
      <li v-for="(member, index) in members" :key="member.id">
        {{ index }} : {{ member }}
      </li>
    </ul>

    <ul>
      <li v-for="value in book2" :key="value">
        {{ value }}
      </li>
    </ul>
    <ul>
      <li v-for="(value, key) in book2" :key="value">
        {{ key }} : {{ value }}
      </li>
    </ul>
    <ul>
      <li v-for="(value, key, index) in book2" :key="value">
        {{index}} : {{ key }} : {{ value }}
      </li>
    </ul>

    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>タイトル</th>
          <th>著者</th>
          <th>URL</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="book in books" :key="book.id">
          <td>{{ book.id }}</td>
          <td>{{ book.title }}</td>
          <td>{{ book.author }}</td>
          <td>{{ book.url }}</td>
        </tr>
      </tbody>
    </table>

    <div v-text="test"></div>
    <div v-html="test"></div>

    <div id="app">

      <div v-cloak>{{ test1 }}</div>
      <div >{{ test2 }}</div>

    <!-- <button onClick="btnClicked()">クリックし</button> -->
    <div>
      <button @click="btnClicked">クリックし</button>
      <button @click="btnClickedEvent">Eventクリックし</button>
      <button @click="btnClickedArgs(1)">引数クリックし</button>
      <button @click="btnClickedArgsEvent(1, $event)">引数クリックし</button>
    </div>

    <form>
      <button @click.prevent="doThis">送信</button>
    </form>
    <br>
    <div>{{ totalPrice }}</div>
    <div>{{ totalPrice }}</div>
    <div>{{ totalPriceMethods() }}</div>
    <div>{{ totalPriceMethods() }}</div>

    </div>

    <p>
      For a guide and recipes on how to configure / customize this project,<br>
      check out the
      <a href="https://cli.vuejs.org" target="_blank" rel="noopener">vue-cli documentation</a>.
    </p>
    <h3>Installed CLI Plugins</h3>
    <ul>
      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-babel" target="_blank" rel="noopener">babel</a></li>
      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-eslint" target="_blank" rel="noopener">eslint</a></li>
    </ul>
    <h3>Essential Links</h3>
    <ul>
      <li><a href="https://vuejs.org" target="_blank" rel="noopener">Core Docs</a></li>
      <li><a href="https://forum.vuejs.org" target="_blank" rel="noopener">Forum</a></li>
      <li><a href="https://chat.vuejs.org" target="_blank" rel="noopener">Community Chat</a></li>
      <li><a href="https://twitter.com/vuejs" target="_blank" rel="noopener">Twitter</a></li>
      <li><a href="https://news.vuejs.org" target="_blank" rel="noopener">News</a></li>
    </ul>
    <h3>Ecosystem</h3>
    <ul>
      <li><a href="https://router.vuejs.org" target="_blank" rel="noopener">vue-router</a></li>
      <li><a href="https://vuex.vuejs.org" target="_blank" rel="noopener">vuex</a></li>
      <li><a href="https://github.com/vuejs/vue-devtools#vue-devtools" target="_blank" rel="noopener">vue-devtools</a></li>
      <li><a href="https://vue-loader.vuejs.org" target="_blank" rel="noopener">vue-loader</a></li>
      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank" rel="noopener">awesome-vue</a></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
        data(){
          return {
            google: 'https://google.com',
            formInput:{
              name: 'your_name',
              placeholder: '名前を設定してくださいね'
            },
            isDisplay: true,
            signal: 'blue',
            members: ['最強','強靭','無敵'],
            book2: {
              title: 'タイトル',
              author: '著者名',
              url: 'https//google.com'
            },
            books:[
              {
                id:1,
                title: 'タイトル1',
                author: '著者名1',
                url: 'https//google.com'
              },
              {
                id:2,
                title: 'タイトル2',
                author: '著者名2',
                url: 'https//google.com'
              },
              {
                id:3,
                title: 'タイトル3',
                author: '著者名3',
                url: 'https//google.com'
              }
            ],
            test: 'あああ <br> いいい',
            test1: 'v-cloakあり',
            test2: 'v-cloakなし',
            price: 1,
            number: 1
          }
        },
        created(){
          console.log('created')
          console.log(this.$el)
        },
        mounted(){
          console.log('created')
          console.log(this.$el)
        },
        methods:{
          btnClicked(){
            console.log('Vue クリックされた')
          },
          doThis(){
            console.log(' クリックされた')
          },
          btnClickedEvent(e){
            console.log(e)
          },
          btnClickedArgs(int){
            console.log(int)
          },
          btnClickedArgsEvent(int, e){
            console.log(int , e);
          },
          totalPriceMethods(){
            console.log('メソッドです')
            return this.number * this.price
          }
        },
        computed: {
          // totalPrice(){
          //   console.log('computedです')
          //   return this.number * this.price
          // }
          totalPrice: app => app.number * app.price
        },
        watch: {}

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
[v-cloak] {
  display: none;
}

</style>
