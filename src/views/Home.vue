<template>
  <div class="home">
    <div class="characters">
      <div
        v-for="character in characterNames"
        :key="character"
        class="character"
        @click="setSelected(character)"
      >{{ character }}</div>
    </div>
    <div class="moves">
      <div v-for="(item, index) in bark" :key="index + 1" class="move">
        <div class="move_number">{{index + 1}}</div>
        <div class="move_information">
          <div class="move_name">{{ item.move }}</div>
          <div class="move_inputs">
            <div v-for="item in item.inputs" :key="item.id" class="input">{{ item }}</div>
          </div>
          <div class="move_types">
            <div v-for="item in item.type" :key="item.id">{{ item }}</div>
          </div>
        </div>
        <div class="move_einformation">
          <div class="start_up">Start: {{item.start_up}}</div>
          <div class="block">Block: {{item.block}}</div>
          <div class="hit">Hit: {{item.nh}}</div>
        </div>
      </div>

      <!-- <p>Inputs: {{item.inputs}}</p>
      <p>Type: {{item.type}}</p>
      <p>Damage: {{item.damage}}</p>
      <p>Start-up: {{item.start_up}}</p>
      <p>Block: {{item.block}}</p>
      <p>NH: {{item.nh}}</p>
      <p>CH: {{item.ch}}</p>
      <p>Total: {{item.total}}</p>-->
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "Home",
  data() {
    return {
      publicPath: process.env.BASE_URL,
      itemCount: 0,
      bark: {},
      selectedCharacter: "alisa",
      characterNames: [
        "gouki",
        "alisa",
        "anna",
        "amking",
        "asuka",
        "bob",
        "bryan",
        "claudio",
        "devil",
        "dragunov",
        "eddy",
        "eliza",
        "fahkumram",
        "feng",
        "ganryu",
        "geese",
        "gigas",
        "heihachi",
        "hwoarang",
        "jack7",
        "jin",
        "josie",
        "julia",
        "katarina",
        "kazumi",
        "kazuya",
        "king",
        "kuma",
        "lars",
        "law",
        "lee",
        "lei",
        "leo",
        "leroy",
        "lili",
        "lucky",
        "marduk",
        "raven",
        "miguel",
        "negan",
        "noctis",
        "nina",
        "paul",
        "shaheen",
        "steve",
        "xiaoyu",
        "yoshimitsu",
        "zafina",
      ],
    };
  },
  methods: {
    upIndex() {
      this.itemCount += 1;
      return this.itemCount;
    },
    setSelected(arg) {
      this.selectedCharacter = arg;
      this.characterData(arg)
    },
    characterData(character) {
      console.log("char", character);
      console.log(window.location.href + "json/" + character + ".json")
      fetch(window.location.href + "json/" + character + ".json")
        .then((res) => res.json())
        .then((dat) => this.bark = dat);
    },
  },
  computed: {
    totalLength() {
      return Object.keys(this.bark).length;
    },
  },
};
</script>

<style scoped>
.home {
  padding: 3%;
  display: flex;
}
.character {
  padding: 1%;
}
.character:hover {
  background-attachment: blue;
}
.characters {
  width: 15%;
  background-color: white;
}
.moves {
  width: 80%;
}
.move {
  width: 100%;
  background-color: #2b3a41;
  display: flex;
  flex-direction: row;
  color: white;
  border: 2px solid gray;
  opacity: 0.98;
  transition: all 0.2s;
}
.move:nth-child(odd) {
  background-color: #2a3139;
}
.move_name {
  text-align: left;
  padding: 2%;
  font-weight: bolder;
}
.move_number {
  width: 50px;
  border-bottom-right-radius: 40%;
  height: fit-content;
  background-color: #323e45;
}
.move_inputs {
  display: flex;
  width: 100%;
  flex-direction: row;
}
.move_types {
  display: flex;
  padding: 3px;
}
.move_information {
  width: 250px;
}
.move_einformation {
  display: flex;
  text-align: right;
  flex-direction: column;
  flex-grow: 1;
  width: 50px;
  justify-content: flex-end;
}
.input {
  padding: 3px;
}
.move:hover {
  background-color: #004f81;
  border-color: #00d9ff;
  box-shadow: 1px 1px 1px 1px #00d9ff;
}
p {
  padding: 0px;
  margin: 0px;
}
</style>