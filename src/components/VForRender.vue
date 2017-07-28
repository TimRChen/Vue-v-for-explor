<template>
  <div class="content">
    <ul class="show-animate">
      <li class="animate">对照组</li>
      <li v-for="(item, key, index) in items" class="animate" :key="judge ? item.id : index">{{item.id}}</li>
    </ul>
    <div class="btn-group">
      <div class="btn">
        <span class="label">改变li绑定的key值====></span>
        <button class="button" @click="judge = !judge">changeKey</button>
      </div>
      <div class="btn">
        <span class="label">改变第一个元素的Id值==></span>
        <button class="button" @click="items[0].id = Math.floor(Math.random()*1000)">changeSomeId</button>
      </div>
      <div class="btn">
        <span class="label">将实验组进行排序====></span>
        <button class="button" @click="items = items.sort((a, b) => a.id - b.id)">changePosition</button>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      judge: false,
      items: [
        {
          id: 2,
        },
        {
          id: 1,
        },
        {
          id: 3,
        },
        {
          id: 4,
        },
      ]
    }
  },
  beforeCreate: function() {
    debugger
  },
  created: function() {
    debugger
  },
  beforeMount: function() {
    debugger
  },
  mounted: function() {
    debugger
  },


  beforeUpdate: function() {
    debugger
  },
  updated: function() {
    debugger
  },
  destroyed: function() {
    debugger
  }

}
</script>
<style>

  .show-animate {
    text-align: center;
  }

  .btn {
    width: 300px;
    margin-bottom: 30px;
    margin-left: 40px;
  }

  .button {
    float: right;
  }

  .animate {
    width: 50px;
    margin-bottom: 20px;
    color: #fff;
    background: seagreen;
    border-radius: 3px;
    animation: animate 3s infinite;
  }

  @keyframes animate
  {
    from {
      width: 50px;
    }
    to {
      width: 300px;
    }
  }


</style>
