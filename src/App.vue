<template>
  <div id="app">
    <div class="panel panel-primary">
      <div class="panel-heading">
        <h3 class="panel-title">添加</h3>
      </div>
      <div class="panel-body form-inline">
        <lable>
          ID:
          <input type="text" class="form-control" v-model="id" />
        </lable>

        <lable>
          Brand:
          <input type="text" class="form-control" v-model="brand" />
        </lable>

        <input type="button" value="添加" class="btn btn-primary" @click="add" />
        <lable>
          搜索：
          <input type="text" class="form-control" v-model="keywords" />
        </lable>
      </div>
    </div>

    <table class="table table-hover">
      <thead>
        <tr>
          <th>ID</th>
          <th>品牌名称</th>
          <th>添加时间</th>
          <th>操作</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in list" :key="item.id">
          <td v-text="item.id"></td>
          <td v-text="item.brand"></td>
          <td v-text="item.ctime"></td>
          <td>
            <a href="#" @click.prevent="del(item.id)" style:color:red>删除</a>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
export default {
  name: 'app',
  data() {
    return {
      id: '',
      brand: '',
      keywords: '',
      list: [],
    };
  },
  methods: {
    add() {
      var car = { id: this.id, brand: this.brand, ctime: new Date() };
      this.list.push(car);
      this.id = this.brand = '';
    },
    del(id) {
      var index = this.list.findIndex(item => {
        if (item.id == id) return true;
      });

      this.list.splice(index, 1);
    },
    search(keywords) {
      var newList = [];
      this.list.forEach(item => {
        if (item.brand.indexOf(keywords) != -1) newList.push(item);
      });
      return newList;
    }
  }
};
</script>
<style lang="scss" scoped>
</style>
