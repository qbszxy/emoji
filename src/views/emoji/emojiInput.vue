<template>
    <div class="emojiInputWrap">
        <div class="inputWrap">
            <el-input :placeholder="palce" :type="type" :row="4" v-model="val" class="input"></el-input>
            <emoji @setIcon="setIcon"></emoji>
        </div>

    </div>
</template>
<script>
import emoji from '../../components/emoji/emoji'
export default {
  props: ['palce', 'type', 'value'],
  data () {
    return {
      // value:this.val,
      // keyName:this.keyName
    }
  },
  computed: {
    val: {
      get () {
        return this.value || ''
      },
      set (value) {
        this.$emit('input', value)
      }
    }
  },
  methods: {
    setIcon (v) {
      // this.insertInputTxt('input',v)
      this.val = this.val + v
      // this.input();
    },
    insertInputTxt (id, insertTxt) {
      var elInput = document.getElementById(id)
      var startPos = elInput.selectionStart
      var endPos = elInput.selectionEnd
      if (startPos === undefined || endPos === undefined) return
      var txt = elInput.value
      var result = txt.substring(0, startPos) + insertTxt + txt.substring(endPos)
      elInput.value = result
      elInput.focus()
      this.$nextTick(() => {
        elInput.selectionStart = startPos + insertTxt.length
        elInput.selectionEnd = startPos + insertTxt.length
      })
    }
    // input(){
    //     this.$emit('input', this.val)
    // }
  },
  components: {
    emoji
  },
  watch: {
    // value(){
    //     this.$emit('input', this.value)
    //     // this.$emit('setValue',)
    // }
  }

}
</script>
<style lang="scss">
.emojiInputWrap{
    .el-textarea__inner{
        font-family: "Microsoft YaHei" !important;
    }
    .el-input__inner{
        font-family: "Microsoft YaHei" !important;
        padding-right: 30px;
    }
    .inputWrap{
        position: relative;
    }
    .el-input,.el-textarea{
        position: relative;

    }
}

</style>
