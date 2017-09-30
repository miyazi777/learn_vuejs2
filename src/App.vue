<style lang="scss">
  @import '../static/styles.css';
  html, body {
    color: #555;
    margin: 0;
    padding: 0;
    height: 100vh;
  }
  #app {
    height: 100%;
    display: flex;
    .contents {
      height: 100%;
      flex-grow: 1;
      overflow: scroll;
      box-sizing: border-box;
    }
  }
</style>


<template>
  <div id="app">
    <nav-link></nav-link>
    <router-view class="contents" :memos="memos" @add="add" @remove="remove"></router-view>
  </div>
</template>

<script>
  import NavLink from './components/NavLink'

  export default {
    name: 'app',
    data() {
      return {
        memos: [
          {
            id: 1,
            text: 'テスト',
            date: '16-10-28',
            tags: ['tag1', 'tag2']
          },
          {
            id: 2,
            text: 'テスト2',
            date: '16-11-28',
            tags: ['tag1', 'tag2']
          },
        ]
      }
    },
	computed: {
	  nextId() {
	    // this.memosの中で一番大きいid + 1を取得
	    return this.memos.reduce((id, memo) => {
	    	return id < memo.id ? memo.id : id
	    }, 0) + 1
      }
	},
	methods: {
		add(newMemo) {
            newMemo.id = this.nextId
            this.memos.push(newMemo)
		},
		remove(id) {
			console.log("id = " + id)
            const index = this.memos.findIndex((memo) => {
				return memo.id === id
			})
			this.memos.splice(index, 1)
		}
	},
  components: {
				NavLink
    }
  }
</script>

