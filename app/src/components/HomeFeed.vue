<template>
  <div class="homefeed">
    <div class="homegroup">
      <div class="creategroup">
        <router-link :to="{ name: 'CreateGroup'}">
          <el-button type="info">グループ作成</el-button>
        </router-link>
      </div>
      <div class="groupfeeds">
        <div class="group-content" style="font-size: 24px">
          <p>{{group[0]['groupname']}}</p>
          <br/>
          <img src="@/assets/avatar.png" alt="avator">
          <p>{{groupfeeds[0]['speaker']}}</p>
          <div class="content">
            <p>{{groupfeeds[0]['content']}}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>

export default {
  name: "HomeFeed",
  data () {
    return {
      group: [],
      groupfeeds: [],
      // groupname: group[0].groupname,
      // speaker: groupfeed[0].speaker
    }
  },
  created:function() {
    this.$store.state.myGroup.forEach((mygroup) => {
      this.$firestore.collection('group').doc(mygroup).get.then((doc) => {
        this.group.push(doc.data().groupname)
      })
    })
  }
}
</script>
<style  scoped>
.group-content {
  text-align: left;
  background-color: YELLOW;
  margin-top: 10px;
}
.content img {
  display:inline-block;
  vertical-align: middle;
}
.content p {
  display: inline;
  vertical-align: middle;
}
</style>
