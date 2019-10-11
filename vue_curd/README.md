### vue实现增删改查
#### show.vue文件（父组件）
```html
<template>
  <div class="container" id="app">
    <div>
      <input type="text" placeholder="search" @input="search" list="cars" class="search" />
      <datalist id="cars">
        <option v-for="(item,index) in searchlist" :value="item" :key="index"></option>
      </datalist>
      <input type="button" class="add" @click="add" value="新增" />
    </div>
    <div>
      <table>
        <tr>
          <th>id</th>
          <th>用户名</th>
          <th>邮箱</th>
          <th>性别</th>
          <th>省份</th>
          <th>爱好</th>
          <th>操作</th>
        </tr>
        <tr v-cloak v-for="(item, index) of slist" :key="index">
          <td>{{ index + 1 }}</td>
          <td>{{ item.username }}</td>
          <td>{{ item.email }}</td>
          <td>{{ item.sex }}</td>
          <td>{{ item.province }}</td>
          <td>{{ item.hobby.join(' | ') }}</td>
          <td>
            <a href="javascript:;" @click="showOverlay(index)">修改</a> |
            <a href="javascript:;" @click="del(index)">删除</a>
          </td>
        </tr>
      </table>
    </div>
    <Mode
      :list="selectedlist"
      :isactive="isActive"
      v-cloak
      @change="changeOverlay"
      @modify="modify"
    ></Mode>
  </div>
</template>
```
```javascript
<script>
import Mode from "./mode"
export default {
  components: {
    Mode
  },
  props: ["id"],
  data() {
    return {
      selected: -1, // 选择了哪条记录
      isActive: false, // 是否显示弹窗
      selectedlist: {}, // 选中的信息
      searchlist: [],
      slist: [],
      list: [
        {
          username: "aaaaa",
          email: "123@qq.com",
          sex: "男",
          province: "北京市",
          hobby: ["篮球", "读书", "编程"]
        },
        {
          username: "bbbbb",
          email: "bbbbbbb@163.com",
          sex: "女",
          province: "河北省",
          hobby: ["弹琴", "读书", "插画"]
        },
        {
          username: "aaabb",
          email: "abababab@qq.com",
          sex: "女",
          province: "重庆市",
          hobby: ["篮球"]
        },
        {
          username: "cccccc",
          email: "123@qq.com",
          sex: "男",
          province: "北京市",
          hobby: ["篮球", "读书", "编程"]
        },
        {
          username: "dddddd",
          email: "bbbbbbb@163.com",
          sex: "女",
          province: "河北省",
          hobby: ["弹琴", "读书", "插画"]
        },
        {
          username: "eeeee",
          email: "abababab@qq.com",
          sex: "女",
          province: "重庆市",
          hobby: ["篮球"]
        }
      ]
    };
  },
  created() {
    this.setSlist(this.list);
  },
  methods: {
    // 获取需要渲染到页面中的数据
    setSlist(arr) {
      this.slist = JSON.parse(JSON.stringify(arr));
    },
    //新增数据
    add() {
      this.selectedlist = {
        username: "",
        email: "",
        sex: "男",
        province: "北京市",
        hobby: []
      };
      this.selected = -1;
      this.isActive = true;
    },
    // delete list in index location 删除数据
    del(index) {
      this.list.splice(index, 1);
      this.setSlist(this.list);
    },
    // 弹出修改数据界面并获取此条详细信息
    showOverlay(index) {
      this.selected = index;
      this.selectedlist = this.list[index];
      this.changeOverlay();
    },
    // 点击保存按钮
    modify(arr) {
      //修改数据情况下
      if (this.selected > -1) {
        this.$set(this.list, this.selected, arr);  //Vue.set(要更改的数据，数据的第几项，更改后的数据)
        this.selected = -1;
      }
      //新增数据情况下
      else {
        this.list.push(arr);
      }
      this.setSlist(this.list);
      this.changeOverlay();
    },
    //显示弹窗
    changeOverlay() {
      this.isActive = !this.isActive;
    },
    // 搜索
    search(e) {
      var v = e.target.value, //e.target指向事件执行时鼠标所点击区域的那个元素
        self = this;
      self.searchlist = [];
      if (v) {
        var ss = [];
        // 过滤需要的数据
        this.list.forEach(function(item) {
          if (item.username.indexOf(v) > -1) {
            if (self.searchlist.indexOf(item.username) == -1) {
              self.searchlist.push(item.username);
            }
            ss.push(item);
          } else if (item.email.indexOf(v) > -1) {
            if (self.searchlist.indexOf(item.email) == -1) {
              self.searchlist.push(item.email);
            }
            ss.push(item);
          }
        });
        this.setSlist(ss); // 将过滤后的数据给了slist
      } else {
        // 没有搜索内容，则展示全部数据
        this.setSlist(this.list);
      }
    }
  }
};
</script>
```
```css
<style>
[v-cloak] {
  display: none;
}
table {
  border: 1px solid #ccc;
  padding: 0;
  border-collapse: collapse;
  table-layout: fixed;
  margin-top: 10px;
  width: 100%;
}
table td,
table th {
  height: 30px;
  border: 1px solid #ccc;
  background: #fff;
  font-size: 15px;
  padding: 3px 3px 3px 8px;
}
table th:first-child {
  width: 30px;
}
.container {
  width: 1000px;
  margin: 10px auto 0;
  font-size: 13px;
  font-family: "Microsoft YaHei";
}
.container .search {
  font-size: 15px;
  padding: 4px;
}
.container .add {
  padding: 5px 15px;
}
</style>
```
#### mode.vue文件（子组件）
```html
<template>
  <div class="overlay" v-show="isactive">
    <div class="con">
      <h2 class="title">新增 | 修改</h2>
      <div class="content">
        <table>
          <tr>
            <td>用户名</td>
            <td>
              <input type="text" v-model="modifylist.username" />
            </td>
          </tr>
          <tr>
            <td>邮箱</td>
            <td>
              <input type="text" v-model="modifylist.email" />
            </td>
          </tr>
          <tr>
            <td>性别</td>
            <td>
              <label>
                <input type="radio" name="sex" value="男" v-model="modifylist.sex" />男
              </label>
              <label>
                <input type="radio" name="sex" value="女" v-model="modifylist.sex" />女
              </label>
              <label>
                <input type="radio" name="sex" value="未知" v-model="modifylist.sex" />未知
              </label>
            </td>
          </tr>
          <tr>
            <td>省份</td>
            <td>
              <select name id v-model="modifylist.province">
                <option value="北京市">北京市</option>
                <option value="河北省">河北省</option>
                <option value="河南省">河南省</option>
                <option value="重庆市">重庆市</option>
                <option value="广东省">广东省</option>
                <option value="辽宁省">辽宁省</option>
              </select>
            </td>
          </tr>
          <tr>
            <td>爱好</td>
            <td>
              <label>
                <input type="checkbox" v-model="modifylist.hobby" value="篮球" />篮球
              </label>
              <label>
                <input type="checkbox" v-model="modifylist.hobby" value="读书" />读书
              </label>
              <label>
                <input type="checkbox" v-model="modifylist.hobby" value="插画" />插画
              </label>
              <label>
                <input type="checkbox" v-model="modifylist.hobby" value="编程" />编程
              </label>
              <label>
                <input type="checkbox" v-model="modifylist.hobby" value="弹琴" />弹琴
              </label>
            </td>
          </tr>
        </table>
        <p>
          <input type="button" @click="changeActive" value="取消" />
          <input type="button" @click="modify" value="保存" />
        </p>
      </div>
    </div>
  </div>
</template>
```
```javascript
<script>
export default {
  props: ["list", "isactive"],
  data() {
    return {};
  },
  computed: {
    modifylist() {
      return this.list;
    }
  },
  methods: {
    changeActive() {
      this.$emit("change");
    },
    modify() {
      this.$emit("modify", this.modifylist);
    }
  },
  watch: {}
};
</script>
```
```css
<style>
[v-cloak] {
  display: none;
}
table {
  border: 1px solid #ccc;
  padding: 0;
  border-collapse: collapse;
  table-layout: fixed;
  margin-top: 10px;
  width: 100%;
}
table td,
table th {
  height: 30px;
  border: 1px solid #ccc;
  background: #fff;
  font-size: 15px;
  padding: 3px 3px 3px 8px;
}
table th:first-child {
  width: 30px;
}
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 6;
  background: rgba(0, 0, 0, 0.7);
}
.overlay td:first-child {
  width: 66px;
}
.overlay .con {
  position: absolute;
  width: 420px;
  min-height: 300px;
  background: #fff;
  left: 50%;
  top: 50%;
  -webkit-transform: translate3d(-50%, -50%, 0);
  transform: translate3d(-50%, -50%, 0);
  padding: 20px;
}
</style>
```