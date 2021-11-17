<template>
  <div>
    <div>
      <el-menu
        :default-active="activeIndex"
        class="el-menu-demo"
        mode="horizontal"
        @select="handleSelect"
        background-color="#74787a"
        text-color="#cdd1c5"
        active-text-color="#ffd04b"
      >
        <el-menu-item class="logo"
          ><router-link to="/">XL-STAR</router-link></el-menu-item
        >
        <el-menu-item index="1" style="margin-left: 10px"
          ><router-link to="/home">博客</router-link></el-menu-item
        >
        <el-menu-item index="2"
          ><router-link to="/blogType">分类专栏</router-link></el-menu-item
        >
        <el-menu-item index="3"
          ><router-link to="/blogTag">标签</router-link></el-menu-item
        >
        <el-menu-item index="4"
          ><router-link to="/message">留言板</router-link></el-menu-item
        >
        <el-menu-item index="5"
          ><router-link to="/blogLinks">友链</router-link></el-menu-item
        >
        <el-menu-item index="6"
          ><router-link to="/blogVideo">视频</router-link></el-menu-item
        >
        <el-menu-item index="7"
          ><router-link to="/blogBook">书籍</router-link></el-menu-item
        >
        <el-menu-item
          index="8"
          v-if="this.$router.currentRoute.path != '/blogSearch/'"
        >
          <div @click="goToSearch">
            <el-input size="small" placeholder="请输入内容" clearable>
              <i slot="prefix" class="el-input__icon el-icon-search"></i>
            </el-input>
          </div>
        </el-menu-item>
        <el-menu-item index="9" v-show="user == null"
          ><router-link to="/login">登录</router-link></el-menu-item
        >
        <el-menu-item index="9" v-show="user != null">
          <el-dropdown
            v-show="user != null"
            class="userInfo"
            @command="commandHandler"
          >
            <!--@command="commandHandler" 点击菜单项触发的事件回调-->
            <span class="el-dropdown-link">
              <i><img :src="user==null ? null : user.avatar" alt="" /></i>
            </span>
            <el-dropdown-menu slot="dropdown">
              <el-dropdown-item command="userInfo">个人中心</el-dropdown-item>
              <el-dropdown-item command="setting">设置</el-dropdown-item>
              <!--disabled:禁用的    divided:有分隔线-->
              <el-dropdown-item command="logout" divided
                >注销登录</el-dropdown-item
              >
            </el-dropdown-menu>
          </el-dropdown>
        </el-menu-item>
      </el-menu>
    </div>
  </div>
</template>
  
  <script>
export default {
  name: "Head",
  data() {
    return {
      activeIndex: "",
      user: JSON.parse(window.sessionStorage.getItem("user")),
    };
  },
  props: ["aIndex"],
  mounted() {
    this.activeIndex = this.aIndex;
  },
  methods: {
    blogsearch(keyword) {
      console.log(keyword);
      this.$router.push("/blogSearch/" + keyword);
    },
    handleSelect(key, keyPath) {
      console.log(key, keyPath);
      // this.activeIndex = key
    },
    goToSearch() {
      this.$router.push("/blogSearch/");
    },
    commandHandler(cmd) {
      //该方法有一个参数，cmd
      if (cmd == "logout") {
        this.$confirm("此操作将注销登录, 是否继续?", "提示", {
          confirmButtonText: "确定",
          cancelButtonText: "取消",
          type: "warning",
        })
          .then(() => {
            this.getRequest("/logout");
            window.sessionStorage.removeItem("user");
            this.$router.replace("/");
          })
          .catch(() => {
            this.$message({
              type: "info",
              message: "已取消注销",
            });
          });
      }
    },
  },
};
</script>
  
  <style scoped>
/* logo */
.logo {
  margin-left: 150px;
  font-size: 30px;
  font-family: 华文行楷;
  color: #409eff !important;
}
/*设置鼠标移上去显示为手指*/
.userInfo {
  cursor: pointer;
}
/* 头像样式 */
.el-dropdown-link img {
  width: 48px;
  height: 48px;
  border-radius: 24px;
  margin-left: 8px;
}
</style>