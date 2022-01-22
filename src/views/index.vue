<template>
  <div class="container">
    <div class="emoji-wrapper">
      <div class="emoji-preview">{{text}}</div>
      <div class="emojiWrap" style="margin-left: 0;">
        <el-popover placement="bottom" title="选择颜文字"  width="800" trigger="click">
          <span class="emoji" style="margin:0"  slot="reference"  @click="clickEmoji">
            <img src="./emoji/icon/add.png" alt="">
          </span>
          <div v-if="visible">
            <el-tabs v-model="activeName" class="emojiPanel">
              <el-tab-pane :label="item.name" :name="item.name" v-for="item in emojiNameList" :key="item.name"></el-tab-pane>
              <el-tooltip :content="icon.name" placement="bottom" effect="light" v-for="(icon,index) in emojiList[activeName]" :key="index" :enterable="false">
                <i :class="[icon.className,'emoji']" @click="getIcon(icon.icon)"></i>
              </el-tooltip>
            </el-tabs>
          </div>
        </el-popover>
      </div>
      <el-input v-model="text" class="input" type="textarea" :rows="5" resize="none"></el-input>
    </div>
  </div>
</template>

<script>
import emojiList from './emoji/icon'

export default {
  data () {
    return {
      activeName: '笑脸与人物',
      emojiShow: false,
      visible: false,
      text: ''
    }
  },
  computed: {
    emojiList () {
      const obj = {}
      for (let i = 0; i < emojiList.length; i++) {
        obj[emojiList[i].name] = emojiList[i].list
      }
      console.log(obj)
      return obj
    },
    emojiNameList () {
      return emojiList.map(v => ({
        name: v.name
      }))
    }
  },
  methods: {
    clickEmoji () {
      this.visible = true
    },
    getIcon (v) {
      this.text = this.text + v
    }
  }
}
</script>

<style lang='scss' scoped>

@import './emoji/emoji.css';
.emojiWrap{
  display: flex;
  align-items: center;
  width: 100%;
  height: 40px;
  padding: 0 8px;
  img{
      width: 17.5px;
      height: 16px;
  }

}
.emojiPanel.el-tabs{
    max-height: 300px;
    overflow-y: auto;
}
.emoji{
    display: inline-block;
    width: 24px;
    height: 24px;
    margin: 5px;
    cursor: pointer;
    border: 1px solid transparent;
    &:hover{
        border: 1px solid #aaa;
    }
}
span.emoji{
    border: 1px solid transparent;
    &:hover{
        border: 1px solid transparent;
    }
}
.container{
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100vh;
  padding: 10px;
  .emoji-wrapper{
    position: relative;
    width: 500px;
    height: 300px;
    border: 1px solid #ccc;
    margin-top: -200px;
    .emoji-preview{
      width: 100%;
      height: 145px;
      font-size: 12px;
      padding: 8px;
      border-bottom: 1px solid #e4e4e4;
    }
    .input{
      position: absolute;
      left: 0;
      bottom: 0;
      /deep/.el-textarea__inner{
        border: 0;
        border-top: 1px solid #e4e4e4;
        padding-left: 8px;
      }
    }
  }
}
</style>
