<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <div class="header q-mb-md">
      <h5 style="margin-bottom: 10px">
        <strong> Welcome Back John, </strong> You have...
      </h5>
      <q-chip square style="margin: -6px">
        <q-avatar
          color="transparent"
          text-color="cyan-8"
          size="lg"
          bg-color="transparent"
          >2</q-avatar
        >
        New Mails
      </q-chip>
    </div>
    <tables />
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import tables from "@/components/table.vue";
export default {
  name: "Home",
  components: {
    HelloWorld,
    tables,
  },
};
</script>
<style >
.header {
  background-image: url("../assets/header.svg");
  height: 200px;
  background-repeat: no-repeat;
  background-size: contain;
  background-color: #e4f5f5;
  padding: 2%;
}
.q-chip {
  background: transparent !important;
}
@media only screen and (max-width: 600px) {
  .header {
    background-image: unset;
    text-align: center;
  }
}
</style>