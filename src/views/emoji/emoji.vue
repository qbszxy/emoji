<template>
    <div class="emojiWrap">
        <el-popover placement="bottom" title="选择颜文字"  width="800" trigger="click">
            <span class="emoji" style="margin:0"  slot="reference"  @click="clickEmoji">
                <img src="./icon/add.png" alt="">
            </span>
            <div v-if="visible">
                <el-tabs v-model="activeName" @tab-click="handleClick"  class="emojiPanel">
                    <el-tab-pane :label="item.name" :name="item.name" v-for="item in emojiNameList" :key="item.name"></el-tab-pane>
                    <el-tooltip :content="icon.name" placement="bottom" effect="light" v-for="(icon,index) in emojiList[activeName]" :key="index" :enterable="false">
                        <i :class="[icon.className,'emoji']" @click="getIcon(icon.icon)"></i>
                    </el-tooltip>
                </el-tabs>
            </div>
        </el-popover>
    </div>
</template>
<script>
// import list from './icon.json'
import emojiList from '@/views/postReply/components/emoji/icon'
export default {
  data () {
    return {
      activeName: '笑脸与人物',
      emojiShow: false,
      visible: false,
      selectList: []
      // emojiList:[],
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
    handleClick (v) {
      console.log(v)
      // this.emojiList = this.$store.getters.emojiList(this.activeName)
    },
    getIcon (v) {
      // console.log(v);
      this.$emit('setIcon', v)
    },
    clickEmoji () {
      this.visible = true
      // console.log(this.$store.getters.emojiList);
      // this.emojiList = this.$store.getters.emojiList(this.activeName)
      // if(this.$store.getters.emojiList.length){
      //     this.emojiList = this.$store.getters.emojiList
      // }else{
      //     // this.emojiList = require('./icon.json');
      //     this.$store.commit('adsEmoji/setEmojiList',this.emojiList)
      // }
      // if(!this.emojiList.length){
      //     this.emojiList = this.$store.getters.emojiList
      // }
    }
  },
  mounted () {

  }
  // beforeMount() {
  // console.log('this.$store.getters.adsEmoji',this.$store.getters.emojiList);
  //     if(this.$store.getters.emojiList.length){
  //         this.emojiList = this.$store.getters.emojiList
  //     }else{
  //         this.emojiList = require('./icon.json');
  //         this.$store.commit('adsEmoji/setEmojiList',this.emojiList)
  //     }

  // },
}
</script>
<style lang="scss">
@import './emoji.css';
.emojiWrap{
    position: absolute;
    right: 10px;
    bottom: 15px;
    width: 20px;
    height: 20px;
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
</style>
