<template>
  <div>
    <el-form>
      <el-form-item
        v-for="(i, index) in obj"
        :key="index"
        :label="labelName[index]"
      >
        <el-checkbox-group @change="finish" v-model="newobj[index]">
          <el-checkbox
            v-for="item in i"
            :key="item"
            :label="item"
            name="tag"
          ></el-checkbox>
        </el-checkbox-group>
      </el-form-item>
    </el-form>

    
    <!-- <button @click.prevent="finish">finish</button> -->
    <!-- <div>{{ tags }}</div> -->
  </div>
</template>

<script>
export default {
  data() {
    return {
      labelName: {
        jsby: "角色扮演：",
        gdqj: "格斗拳击：",
        yzxx: "益智休闲：",
        cltf: "策略塔防：",
        qpkp: "棋牌卡片：",
        scjs: "赛车竞速：",
        mnjy: "模拟经营：",
        dzpk: "动作跑酷：",
        mxjm: "冒险解谜：",
        ylyc: "娱乐养成：",
        tyyd: "体育运动：",
        fxsj: "飞行射击：",
        yyjp: "音乐节拍：",
      },
      newobj: {
        jsby: [],
        gdqj: [],
        yzxx: [],
        cltf: [],
        qpkp: [],
        scjs: [],
        mnjy: [],
        dzpk: [],
        mxjm: [],
        ylyc: [],
        tyyd: [],
        fxsj: [],
        yyjp: [],
      },
      obj: {
        jsby: ["角色扮演", "仙侠", "修仙", "模拟", "恋爱", "魔幻","热血",'传奇'],
        gdqj: ["拳击", "格斗", "动作", "竞技"],
        yzxx: ["休闲", "养成", "益智", "脑力", "解压", "魔性", "搞笑"],
        cltf: ["策略", "塔防", "冒险", "战争"],
        qpkp: ["卡牌", "策略", "回合制", "桌游"],
        scjs: ["赛车", "竞速", "驾驶", "模拟"],
        mnjy: ["模拟", "经营", "美食", "养成", "休闲"],
        dzpk: ["动作", "跑酷", "闯关"],
        mxjm: ["冒险", "解密", "地牢", "恐怖", "推理", "惊悚", "动作", "像素"],
        ylyc: ["娱乐", "养成", "休闲"],
        tyyd: ["体育", "篮球", "足球", "运动", "健身"],
        fxsj: ["射击", "飞行", "模拟", "闯关",'枪战'],
        yyjp: ["音乐", "指尖", "节奏", "吉他", "趣味"],
      },
      tags: [],
    };
  },
  methods: {
    finish() {
      this.tags = [];
      // 选中最多多选框的类别
      let category = null;
      let thelong = 0;
      Object.keys(this.newobj).forEach((item) => {
        if (this.newobj[item].length !== 0) {
          if (this.newobj[item].length > thelong) {
            thelong = this.newobj[item].length;
            category = item;
          }

          this.tags.push(...this.newobj[item]);
        }
      });
      console.log(category);
      // 选中的所有多选框
      console.log(this.tags);

      this.tags = Array.from(new Set(this.tags));
      let obj = {
        category,
        tags: this.tags,
      };
      this.$emit("finish", obj);
    },
  },
};
</script>

<style></style>
