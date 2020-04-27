<template>
  <div id="calc" class="w-100 bg-white border shadow" :class="'border-' + borderColor">
    <div class="form-group border-bottom mb-0" :class="'border-' + borderColor">
      <input
        readonly
        type="text"
        id="textbox"
        placeholder="0"
        v-model.trim="textBox"
        class="form-control form-control-lg bg-white border-0 text-right py-5"
      />
    </div>
    <div class="p-3">
      <div class="row p-1">
        <button @click="clearMem" aria-role="button" class="col btn btn-outline-danger p-3 m-1">C</button>
        <button @click="del" class="col btn btn-outline-warning p-3 m-1">DEL</button>
        <button @click="digitClicked(' / ')" class="col btn btn-outline-info p-3 m-1">/</button>
      </div>

      <div class="row p-1">
        <button @click="digitClicked('7')" class="col btn btn-outline-dark p-3 m-1">7</button>
        <button @click="digitClicked('8')" class="col btn btn-outline-dark p-3 m-1">8</button>
        <button @click="digitClicked('9')" class="col btn btn-outline-dark p-3 m-1">9</button>
        <button @click="digitClicked(' * ')" class="col btn btn-outline-info p-3 m-1">X</button>
      </div>

      <div class="row p-1">
        <button @click="digitClicked('4')" class="col btn btn-outline-dark p-3 m-1">4</button>
        <button @click="digitClicked('5')" class="col btn btn-outline-dark p-3 m-1">5</button>
        <button @click="digitClicked('6')" class="col btn btn-outline-dark p-3 m-1">6</button>
        <button @click="digitClicked(' - ')" class="col btn btn-outline-info p-3 m-1">-</button>
      </div>

      <div class="row p-1">
        <button @click="digitClicked('1')" class="col btn btn-outline-dark p-3 m-1">1</button>
        <button @click="digitClicked('2')" class="col btn btn-outline-dark p-3 m-1">2</button>
        <button @click="digitClicked('3')" class="col btn btn-outline-dark p-3 m-1">3</button>
        <button @click="digitClicked(' + ')" class="col btn btn-outline-info p-3 m-1">+</button>
      </div>

      <div class="row p-1">
        <button @click="digitClicked('0')" class="col btn btn-outline-dark p-3 m-1">0</button>
        <button @click="digitClicked('.')" class="col btn btn-outline-dark p-3 m-1">.</button>
        <button @click="equalTo" class="col btn btn-outline-success p-3 m-1">=</button>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  data: function() {
    return {
      textBox: "0",
      borderColor: "dark"
    };
  },

  methods: {
    clearMem: function() {
      this.textBox = "0";
      this.borderColor = "dark";
    },

    del: function() {
      try {
        this.textBox = this.textBox
          .trim()
          .slice(0, -1)
          .trim();
      } catch {
        this.clearMem(); // Force clear if error occur
      }
    },

    digitClicked: function(value) {
      if (this.textBox == 0) {
        this.textBox = value;
      } else {
        this.textBox = this.textBox + value;
      }
    },

    equalTo: function() {
      try {
        this.borderColor = "dark";
        this.textBox = eval(this.textBox.toString());
        this.borderColor = "success";
      } catch (err) {
        this.borderColor = "danger";
      }
    },

    getKeyPressed: function(evt = KeyboardEvent) {
      const digitKeys = ["0", "1", "2", "3", "4", "5", "6", "7", "8", "9", "."];
      const actionKeys = ["+", "-", "*", "x", "/", "", "Enter", "Backspace"];

      if (digitKeys.includes(evt.key)) {
        this.digitClicked(evt.key);
      } else if (actionKeys.includes(evt.key)) {
        switch (evt.key) {
          case "x":
            this.digitClicked(" * ");
            break;

          case "Backspace":
            this.del();
            break;

          case "Enter":
            this.equalTo();
            break;

          default:
            this.digitClicked(" " + evt.key + " ");
            break;
        }
      }
    }
  }
};
</script>


<style scoped>
#calc {
  max-width: 420px;
}

.btn:focus,
button:focus {
  outline: none;
}
</style>