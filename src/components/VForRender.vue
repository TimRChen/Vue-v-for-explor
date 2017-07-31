<template>
  <div class="content">
    <div class="header">
      <h3>v-for响应式key, index及item.id参数对v-bind:key值造成差异研究</h3>
    </div>
    <ul class="show-animate">
      <li class="animate">对照组</li>
      <li v-for="(item, key, index) in items" class="animate" :key="judge ? item.id : key">{{item.id}}</li>
    </ul>
    <div class="btn-group">
      <div class="btn">
        <span class="label">改变第一个元素的Id值==></span>
        <button class="button" @click="items[0].id = Math.floor(Math.random()*1000)">changeSomeId</button>
      </div>
      <div class="btn">
        <span class="label">将实验组进行排序====></span>
        <button class="button" @click="items = items.sort((a, b) => a.id - b.id)">changePosition</button>
      </div>
      <div class="btn">
        <span class="label">改变li绑定的key值====></span>
        <button class="button" @click="judge = !judge">changeKey</button>
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
    console.log('beforeCreate..')
    // debugger
  },
  created: function() {
    console.log('created..')
    // debugger
  },
  beforeMount: function() {
    console.log('beforeMount..')
    // debugger
  },
  mounted: function() {
    console.log('mounted..')
    // debugger
  },


  beforeUpdate: function() {
    console.log('beforeUpdate..')
    // debugger
  },
  updated: function() {
    console.log('updated..')
    // debugger
  },
  destroyed: function() {
    console.log('destroyed..')
    // debugger
  }

}
</script>
<style>
    
    .header {
      margin-left: 40px;
    }

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
    animation: animate 5s infinite;
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
