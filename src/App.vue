<template>
  <div class="container p-2 mt-5">
    <h1 class="comprer fw-bold display-5">
      Compr<i class="bg-gradient">e</i>r.
    </h1>
    <b-badge class="bg-none appinfo comprer">HASH STRING COMPARE TOOL</b-badge>
    <div class="inputContainer">
      <b-textarea
        ref="h01"
        class="inputbox form-control mb-3 border-0 font-monospace text-secondary form-control-lg"
        type="text"
        placeholder="HASH 01"
        v-model="hash1"
        :disabled="showClass"
        @paste="focusMe"
      />
      <b-textarea
        ref="h02"
        class="inputbox form-control border-0 font-monospace text-secondary form-control-lg"
        type="text"
        placeholder="HASH 02"
        v-model="hash2"
        :disabled="showClass"
        @paste="runComplr"
      />
    </div>
    <button
      class="w-25 my-4 btn bg-gradient compareButton"
      @click="
        hashLength();
        compr();
        showCompr();
        isMatch();
      "
    >
      Compare
    </button>
    <button
      class="mx-2 btn clearButton bg-gradient hiddenClass"
      :class="{ visibleClass: showClass }"
      @click="
        clearAll();
        focusOnload();
      "
    >
      + New
    </button>

    <div
      class="position-relative mt-4 hiddenClass"
      :class="{ visibleClass: showClass }"
    >
      <div v-if="hash1 === hash2" class="my-3 text-success h3">
        It's a Match!
      </div>
      <div v-else-if="hash1 !== hash2" class="my-3 text-danger h3">
        Data Doesn't Match!
      </div>
      <div id="dd" class="text-light">
        <span class="charBadge badge bg-dark text-secondary">
          {{ hash1.length }}
        </span>
        <span class="badge bg-none text-secondary">HASH 01</span>
        <!-- HASH 01 -->
        <ul class="hashholder">
          <li
            class="d-inline-flex font-monospace"
            v-for="item in this.hash1"
            :key="item"
          >
            {{ item }}
          </li>
        </ul>
        <ul class="marker">
          <li
            class="d-inline-flex bg-gradient font-monospace"
            :class="item"
            v-for="item in this.checkStr"
            :key="item"
          >
            {{ item }}
          </li>
        </ul>
      </div>
      <div id="dc" class="text-light">
        <span class="charBadge badge bg-dark text-secondary">
          {{ hash2.length }}
        </span>
        <span class="badge bg-none text-secondary">HASH 02</span>
        <!-- HASH 02 -->
        <ul class="hashholder">
          <li
            class="d-inline-flex font-monospace"
            v-for="item in this.hash2"
            :key="item"
          >
            {{ item }}
          </li>
        </ul>
        <ul class="marker">
          <li
            class="d-inline-flex bg-gradient font-monospace"
            :class="item"
            v-for="item in this.checkStr"
            :key="item"
          >
            {{ item }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data: () => ({
    hash1: "",
    hash2: "",
    checkStr: [],
    infoMsg: "",
    showClass: false,
    maxHash: "0",
  }),
  methods: {
    showCompr: function () {
      if (this.checkStr.length !== 0) {
        this.showClass = true;
      } else {
        this.showClass = false;
      }
    },
    compr: function () {
      if (
        this.checkStr.length === 0 &&
        this.hash1 !== "" &&
        this.hash2 !== ""
      ) {
        for (let i = 0; i < this.maxHash; i++) {
          this.hash1[i] === this.hash2[i]
            ? this.checkStr.push("i")
            : this.checkStr.push("x");
        }
      }
    },
    clearAll: function () {
      this.hash1 = "";
      this.hash2 = "";
      this.checkStr = [];
      this.infoMsg = "";
      this.showClass = false;
    },
    hashLength: function () {
      this.hash1.length > this.hash2.length
        ? (this.maxHash = this.hash1.length)
        : (this.maxHash = this.hash2.length);
    },
    focusMe() {
      var that = this;
      setTimeout(function () {
        that.$refs.h02.$el.focus();
      }, 500);
    },
    focusOnload() {
      var that = this;
      setTimeout(function () {
        that.$refs.h01.$el.focus();
        that.$refs.h01.$el.placeholder = "> Simply paste first line";
        that.$refs.h02.$el.placeholder = "> Than second line";
      }, 1000);
    },
    runComplr() {
      setTimeout(() => {
        this.hashLength();
        this.compr();
        this.showCompr();
        this.isMatch();
      }, 500);
    },
  },
  created() {
    this.focusOnload();
  },
  computed: {},
  components: {},
};
</script>
