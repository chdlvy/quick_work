<template>
  <div id="app">
    <el-form ref="form" :model="form" label-width="120px">
      <el-form-item label="软件原名">
        <el-input v-model="form.softName"></el-input>
        <el-checkbox-group v-model="form.last_softName">
          <el-checkbox label="手游" name="last_softName"></el-checkbox>
          <el-checkbox label="游戏" name="last_softName"></el-checkbox>
          <el-checkbox label="最新版" name="last_softName"></el-checkbox>
          <el-checkbox label="破解版" name="last_softName"></el-checkbox>
          <el-checkbox label="2022" name="last_softName"></el-checkbox>
        </el-checkbox-group>
        <el-input v-model="form.cus_last_softName" placeholder="自定义软件全名(包含长尾词)"></el-input>

      </el-form-item>
      <div>软件名：{{ getSoftName }}</div>
      <el-form-item label="seo标题长尾词">
        <el-checkbox-group v-model="form.title">
          <el-checkbox label="手游" name="title"></el-checkbox>
          <el-checkbox label="游戏" name="title"></el-checkbox>
          <el-checkbox label="最新版" name="title"></el-checkbox>
          <el-checkbox label="手机版" name="title"></el-checkbox>
          <el-checkbox label="安卓版" name="title"></el-checkbox>
        </el-checkbox-group>
        <el-input v-model="form.cus_title" placeholder="自定义"></el-input>
        <div>seo标题：{{ getSeoTitle }}</div>
        <div>{{ form.cus_title == "" ? form.title : form.cus_title }}</div>
        <div>关键字：{{ getKeyWord }}</div>
      </el-form-item>

      <el-form-item label="标签">
        <el-select v-model="value" placeholder="请选择">
          <el-option
            v-for="item in options"
            :key="item.value.cgory"
            :label="item.label"
            :value="item.value.cgory"
          >
          </el-option>
        </el-select>
      <div>{{selectMsg}}</div>

        <category @finish="finish"></category>

      </el-form-item>
      <!-- <category @finish="finish"></category> -->
    </el-form>

     <el-button type="primary" @click="create">生成</el-button>

     <el-input
      type="textarea"
      :rows="50"
      placeholder="请输入内容"
      v-model="textarea">
    </el-input>
  </div>
</template>

<script>
import Category from "./components/category.vue";
export default {
  name: "App",
  components: { Category },
  data() {
    return {
      textarea:'',
      form: {
        softName: "",
        title: [],
        cus_title: "",
        last_softName: [],
        cus_last_softName:'',
        tags: [],
      },
      options: [
        {
          value: {
            id:3,
            text: '安卓游戏 > 角色扮演',
            cgory: 'jsby'
          },
          label: "角色扮演",
        },
        {
          value: {
            id:7,
            text: '安卓游戏 > 格斗拳击',
            cgory: 'gdqj'
          },
          label: "格斗拳击",
        },
        {
          value: {
            id:8,
            text: '安卓游戏 > 益智休闲',
            cgory: 'yzxx'
          },
          label: "益智休闲",
        },
        {
          value:  {
            id:9,
            text: '安卓游戏 > 策略塔防',
            cgory: 'cltf'
          },
          label: "策略塔防",
        },
        {
          value: {
            id:10,
            text: '安卓游戏 > 棋牌卡片',
            cgory: 'qpkp'
          },
          label: "棋牌卡片",
        },
        {
          value:  {
            id:11,
            text: '安卓游戏 > 赛车竞速',
            cgory: 'scjs'
          },
          label: "赛车竞速",
        },
        {
          value:  {
            id:12,
            text: '安卓游戏 > 模拟经营',
            cgory: 'mnjy'
          },
          label: "模拟经营",
        },
        {
          value:  {
            id:20,
            text: '安卓游戏 > 动作跑酷',
            cgory: 'dzpk'
          },
          label: "动作跑酷",
        },
        {
          value:  {
            id:21,
            text: '安卓游戏 > 冒险解谜',
            cgory: 'mxjm'
          },
          label: "冒险解谜",
        },
        {
          value:  {
            id:22,
            text: '安卓游戏 > 娱乐养成',
            cgory: 'ylyc'
          },
          label: "娱乐养成",
        },
        {
          value: {
            id:23,
            text: '安卓游戏 > 体育运动',
            cgory: 'tyyd'
          },
          label: "体育运动",
        },
        {
          value:  {
            id:24,
            text: '安卓游戏 > 飞行射击',
            cgory: 'fxsj'
          },
          label: "飞行射击",
        },
        {
          value:  {
            id:25,
            text: '安卓游戏 > 音乐节拍',
            cgory: 'yyjp'
          },
          label: "音乐节拍",
        },
        {
          value:  {
            id:26,
            text: '安卓游戏 > 其他游戏',
            cgory: 'qtyx'
          },
          label: "其他游戏",
        },
      ],
      value: "",
      selectMsg:{}
    };
  },
  methods: {
   finish(payload) {
    this.selectMsg = this.options.find(item => {
      return item.value.cgory === payload.category
    });
    if(this.selectMsg) {
    this.selectMsg = this.selectMsg.value
    this.value = this.selectMsg.cgory
    }
    else {
      this.value = this.selectMsg
    }
    // this.value = payload.category
    this.form.tags = payload.tags
   },
  //  点击生成
   create() {
    console.log(this.selectMsg);
    this.textarea = `(function (soft_name, name_longlast, seo_Title, key_words, tags,select_id, select_text) {
                let softName = document.querySelector("input[name='Name']")
                let seoTitle = document.querySelector("input[name='SeoTitle']")
                let keyWord = document.querySelectorAll("input[name='Keyword']")
                let aTag = document.querySelectorAll("input[name='Tag']")
                let selectId = document.getElementById("categoryID");
                let selectText = document.getElementById("categoryText");
                // 软件名称
                softName.value = soft_name+name_longlast.join('');
                console.log(soft_name+name_longlast.join(''));
                // seo标题
                seoTitle.value=seo_Title

                // 关键字
                key_words.forEach((item,index)=> {
                    keyWord[index].value = item
                })

                // 标签
                aTag[0].value = soft_name
                tags.forEach((item,index)=> {
                    if(index!==0) {
                        aTag[index].value = tags[index-1]
                    }
                    
                })

                selectId.value = select_id;
                selectText.innerHTML = select_text
            })('${this.form.softName}',${JSON.stringify(this.form.last_softName)},'${this.getSeoTitle}',${JSON.stringify(this.getKeyWord)},${JSON.stringify(this.form.tags)},${this.selectMsg.id},'${this.selectMsg.text}')`
   }
  },
  computed: {
    // 获取软件名
    getSoftName() {
      // let cus_last_softName = this.form.cus_last_softName == ""? this.form.last_softName:this.form.cus_last_softName;
      // let arr = []
      // if(cus_last_softName instanceof Array) {
      //   arr = cus_last_softName.join("");
      // }
      // else {
      //   cus_last_softName = cus_last_softName.split('-')
      //   arr = cus_last_softName.join("");

      // }
      return this.form.softName + this.form.last_softName;
    },
    getSeoTitle() {
      let seoTitle = this.form.cus_title == "" ? this.form.title : this.form.cus_title;
      if (seoTitle instanceof Array) {
        let arr = this.form.last_softName.concat(seoTitle)
        seoTitle = Array.from(new Set(arr)).join('')
      }else {
        // 自定义时各个种类用-分割
        seoTitle= seoTitle.split('-')
        let arr = this.form.last_softName.concat(seoTitle)
        seoTitle = Array.from(new Set(arr)).join('')
      }
      return this.getSoftName + "-" +this.form.softName+this.form.cus_last_softName+seoTitle + "下载";
    },
    getKeyWord() {
      let newarr = [];
      // 这里是seo标题中-后面的内容
      if(this.form.cus_title=='') {
        newarr = this.form.last_softName.concat(this.form.title);
      }else {
        // 如果是自定义的话输入的不同模块的内容用-分割
        newarr = this.form.last_softName.concat(this.form.cus_title.split('-'));
      }
      // 查重和在数组的开头插入软件名
        newarr = Array.from(new Set(newarr));
        newarr.unshift(this.form.softName)

        for(let i = 1;i<newarr.length;i++) {
          newarr[i] = newarr[i-1]+newarr[i]
        }
      return newarr;
    },
  },
};
</script>

<style>
</style>
