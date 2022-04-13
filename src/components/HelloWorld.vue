<template>
  <div>
    <!-- <h1>个人信息：</h1>
    姓：<input type="text" v-model="person.a" />
    <br />
    名：<input type="text" v-model="person.b" />
    <br />
    <span>全名:{{ person.fullname }}</span>
    <slot name="zxd"></slot>
    <br />
    全名：<input type="text" v-model="person.fullname" /> -->

    <h1>当前求和：{{ sum }}</h1>
    <button @click="sum++">点我+1</button>
    <hr />
    <h1>信息：{{ msg }}</h1>
    <button @click="msg += '-'">点我+1</button>
    <hr />
    <h2>年龄：{{ person.name }}</h2>
    <h2>姓名：{{ person.age }}</h2>
    <h2>工作：{{ person.job }}</h2>

    <button @click="person.age++">修改年龄</button>
    <button @click="person.name += '-'">修改姓名</button>

    <button @click="person.job.salary += 1">修改薪资</button>
  </div>
</template>

<script>
import { reactive, computed, ref, watch } from "vue";

export default {
  name: "HelloWorld",
  // props: ["msg", "school"],
  watch: {
    // sum(newvalue, oldvalue) {
    //   console.log("sum变化了", newvalue, oldvalue);
    // },
    // sum: {
    //   immediate: true,
    //   handler(newvalue, oldvalue) {
    //     console.log("sum变化了", newvalue, oldvalue);
    //   },
    //   deep:true
    // },
  },

  setup(props, context) {
    let sum = ref(0);
    let msg = ref("你好哇");
    console.log(context.slots);
    // let person = reactive({
    //   a: "张",
    //   b: "三",
    // });

    // //简谐计算属性
    // person.fullname = computed(() => {
    //   return person.a + "-" + person.b;
    // });

    // 可修改的计算属性
    // person.fullname = computed({
    //   get() {
    //     return person.a + "-" + person.b;
    //   },
    //   set(value) {
    //     const nameArr = value.split("-");
    //     person.a = nameArr[0];
    //     person.b = nameArr[1];
    //   },
    // });

    // 普通数据
    // let name = "张三";
    // let age = 18;

    //  ref （reference） 定义响应式数据
    //  基本类型数据 底层用defineproperye
    // 对象类型数据  -reactive - proxy
    // let name = ref("张三");
    // let age = ref("18");
    // let job = ref({
    //   type: "前端工程师",
    //   salary: "30k",
    // });

    // reactive 定义[对象类型]的响应数据
    // let job = reactive({
    //   type: "前端工程师",
    //   salary: "30k",
    //   a: {
    //     b: {
    //       c: 666,
    //     },
    //   },
    // });
    // let hobby = ["抽烟", "喝酒", "汤头"];

    // 套路： reactive 返回对象体
    let person = reactive({
      name: "张三",
      age: "18",
      job: {
        type: "前端工程师",
        salary: "30k",
      },
      hobby: ["抽烟", "喝酒", "汤头"],
    });
    // function changeinfo() {
    //   person.name = "历史";
    //   // age.value = 30;
    //   // job.value.type = "老板";
    //   // job.value.salary = "60k";
    //   person.hobby[0] = "学习";
    // }

    // function addsex() {
    //   person.sex = "男";
    // }

    // function deletesex() {
    //   delete person.name;
    // }

    // function test() {
    //   context.emit("hello", 666);
    // }

    // 监听ref 定义的一个相应数据
    // watch(
    //   sum,
    //   (newvalue, oldvalue) => {
    //     console.log("sum变化了", newvalue, oldvalue);
    //   },
    //   { immediate: true }
    // );
    // 多个属性监听
    // watch([sum, msg], (newvalue, oldvalue) => {
    //   console.log("sum变化了", newvalue, oldvalue);
    // });
    /*
    reactive对象监听 无法正确获取旧的数据
    默认开启deep :true 且关不掉
    */
    // watch(person, (newvalue, oldvalue) => {
    //   console.log("sum变化了", newvalue, oldvalue);
    // });
    // 只监听其中的某个属性（函数形式）
    // watch(
    //   () => person.age,
    //   (newvalue, oldvalue) => {
    //     console.log("sum变化了", newvalue, oldvalue);
    //   }
    // );

    // 多个属性
    // watch([() => person.age, () => person.name], (newvalue, oldvalue) => {
    //   console.log("sum变化了", newvalue, oldvalue);
    // });

    //特殊情况 只监听其中的一个属性，所以需要配置deep
    watch(
      () => person.job,
      (newvalue, oldvalue) => {
        console.log("job变化了", newvalue, oldvalue);
      },
      { deep: true }
    );

    return {
      // name,
      // age,
      // changeinfo,
      // job,
      // hobby,
      // person,
      // addsex,
      // deletesex,
      // test,
      person,
      sum,
      msg,
    };

    //
    // return () => h("h1", "hello world");
  },
  // components: {
  //   HelloWorld
  // }
};
</script>
