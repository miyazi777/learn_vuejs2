<style scoped>
  input:disabled {
		border-color: transparent;
  }
</style>

<template>
    <div class="editor-view">
      <div>
        <div v-if="memo">
          <label>ID</label>
          <input v-model="input.id" disabled>
        </div>
      </div>
      <div>
          <label>内容:</label>
	        <input v-model="input.text" placeholder="メモのタイトル">
    	</div>
		  <div>
		    <label>日付:</label>
		    <input type="date" v-model="input.date">
        </div>
	    <div>
		    <label>タグ:</label>
            <input v-model="input.tags" placeholder="空白区切りで指定">
		  </div>
	    <div>
        <button @click="cancel" v-if="memo">戻る</button>
		    <button @click="save">保存</button>
	    </div>
    </div>
</template>

<script>
    export default{
			created() {
				this.setMemo()
			},
			props: {
				memo: Object
			},
      data() {
          return {
              input: {
                  text: '',
                  date: '',
                  tags: ''
              }
          }
      },
	    computed: {
		    tagsArr() {
			    return this.input.tags.trim() !== '' ? this.input.tags.trim().split(/\s+/) : []
		    }
	    },
			watch: {
				memo: 'setMemo'
			},
	    methods: {
				setMemo() {
					if (this.memo) {
						Object.assign(this.input, this.memo, {tags: this.memo.tags.join(' ')})
					}
				},
		    save() {
			    // this.inputのクローンを生成する
			    const data = Object.assign({}, this.input, {tags: this.tagsArr})
			    this.$emit('add', data)
		    },
		    cancel() {
			    this.$emit('cancel')
			}
	    }
    }
</script>

