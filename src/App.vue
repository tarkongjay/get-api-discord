<template>
  <div>
    <header>
      <div>
         {{list.name}}
      </div>
      <div>จำนวนคนออนไลน์ : {{ list.presence_count }}</div>
    </header>
    <section class="content-box">
      <div class="lii" v-for="item in listMember" :key="item.id">
        <img :src="item.avatar_url" />
        <div>
          <h1>{{ item.username }}</h1>
          <div v-if="item.status == 'online'">
            <label>💚 ออนไลน์</label>
          </div>
          <div v-if="item.status == 'idle'">
            <label>🧡 ไม่อยู่</label>
          </div>
          <div v-if="item.status == 'dnd'"> 
            <label>💗 ห้ามรบกวน</label>
          </div>
          <div v-for="i in item.game" :key="i.id">
            <label>กำลังเล่น : {{ i }}</label>
          </div>
        </div>
        <div></div>
      </div>
    </section>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",
  data() {
    return {
      list: [],
      listMember: [],
    };
  },
  async mounted() {
    let result = await axios.get(
      "https://discord.com/api/guilds/610745244568387585/widget.json"
    );
    // console.warn(result.data)
    this.list = result.data;
    this.listMember = result.data.members;
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Kanit");
* {
  box-sizing: border-box;
  font-family: "Kanit", sans-serif;
}
body {
  margin: 0;
  background-color: rgb(58, 58, 58);
}
header {
  padding: 1ex;
  margin: 1ex;
  font-size: 7ex;
  text-align: center;
  font-weight: bold;
  color: white;
}
.content-box {
  margin: 5ex;
  padding: 5ex;
  border-radius: 1ex;
  text-align: center;
}
img {
  width: 200px;
  height: 200px;
  border-radius: 20ex;
}
label {
  color: rgb(185, 185, 185);
  font-size: 4ex;
}
.lii {
  border-bottom: 2px solid rgb(116, 116, 116);
  padding: 3ex;
  margin: 3ex;
}
h1{
  color: white;
  font-size: 5ex;
}
</style>
