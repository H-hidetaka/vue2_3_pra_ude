<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p v-if="errors.length">
      <ul>
        <li class="error" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
    <form @submit.prevent="validate">
      氏名
      <input type="text" v-model="yourName">
      <br>
      <p :class="{error: hasError.yourName}">{{ contact.yourName.length}}/20</p>
      <p v-show="hasError.yourName" class="error">氏名は２０文字以内で入力してください</p>
      電話番号
      <input type="tel" v-model.number="contact.tel">
      <br>
      メールアドレス
      <input type="email" v-model.lazy="contact.email">
      <br>
      性別
      <input type="radio" value="male" v-model="contact.gender">男性
      <input type="radio" value="female" v-model="contact.gender">女性
      <input type="radio" value="other" v-model="contact.gender">その他
      <br>
      年齢
      <select v-model="contact.age">
        <option disabled value="">年齢を選択してください</option>
        <option>10代</option>
        <option>20代</option>
        <option>30代</option>
        <option>40代</option>
      </select>
      <br>
      メッセージ
      <textarea v-model="contact.message"></textarea>
      <br>
      注意事項に同意する
      <input type="checkbox" value="webサイト" v-model="contact.attracts">webサイト
      <input type="checkbox" value="チラシ" v-model="contact.attracts">チラシ
      <input type="checkbox" value="その他" v-model="contact.attracts">その他
      <br>
      注意事項に同意する
      <input type="checkbox" v-model="contact.caution">
      <br>
      <input type="submit" value="送信">
    </form>
    <input type="text" v-model="newItem">
    <button @click.prevent="addItem">追加</button>
    <input v-model="query"> 検索

    <ul v-cloak>
      <li v-for="(todo, index) in filteredList" v-bind:key="todo">
      <input type="checkbox" v-model="todo.isDone">
      <span :class="{done: todo.isDone }">{{ todo.item }}</span>
      <button @click="deleteItem(index)">削除</button>
      </li>
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
      newItem:'',
      todos: [],
      query:'',
      contact: {
        yourName: '',
        tel: '',
        email: '',
        gender: '',
        age: '',
        message: '',
        attracts: [],
        caution: false
      },
      errors: [],
      hasError:{
        yourName: false
      }
    }
  },
  methods: {
    addItem(){
      if(!this.newItem) return
      const todo = {
        item: this.newItem,
        isDone: false
      }
      this.todos.push(todo)
      this.newItem = ''
    },
    deleteItem(index){
      this.todos.splice(index, 1)
    },
    validate() {
      this.errors = []
      if(!this.contact.yourName){
        this.errors.push('氏名は必須です')
      }else if(this.contact.yourName.length > 20){
        this.errors.push('氏名は２０文字以内で入力してください')
      }
      if(!this.contact.gender){
        this.errors.push('性別を選択してください')
      }
      if(!this.contact.caution){
        this.errors.push('注意事項にチェックを入れてください')
      }
      if(!this.errors.length){
        console.log('送信可能です')
      }
    }
  },
  computed: {
    filteredList(){
      let that = this
      return this.todos.filter( todo => {
        return todo.item.indexOf(that.query) !== -1
      })
    },
    yourName:{
      get(){
        return this.contact.yourName
      },
      set(value){
        if(value.length <= 20){
          this.hasError.yourName = false
        }else{
          this.hasError.yourName = true
        }
        return this.contact.yourName = value
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.error{
  color: red;
}

ul{
  list-style: none;
}
.done{
  text-decoration: line-through;
}
[v-cloak]{
  display: none;
}
</style>
