<template>
  <div class="home">
    <h1 class="header">Tekken 7 Prettier Movelist</h1>
    <div class="characters">
      <div
        v-for="character in characterNames"
        :key="character"
        class="character"
        @click="setSelected(character)"
        :class="{active: selectedCharacter == character}"
      >{{ character }}</div>
    </div>
    <transition mode="out-in" name="component-fade">
      <div v-if="loading" class="loading" key="loading">
        <h1>Loading</h1>
      </div>
      <div v-else class="moves" key="loaded">
        <div v-for="(item, index) in bark" :key="index + 1" class="move">
          <div class="move_number">{{index + 1}}</div>
          <div class="move_information">
            <div class="move_name">{{ item.move }}</div>
            <div class="move_inputs">
              <div v-for="item in item.inputs" :key="item.id" class="input">
                <!-- <img class="item" v-if="isItem(item)" :src="require('../assets/' + item + '.svg')" /> -->
                
                <img v-if="isItem(item)" :src="require('../assets/' + item + '.svg')" class="inputs"/>
                <div v-else>{{item}}</div>
              </div>
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
      </div>
    </transition>
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
      loading: true,
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
  mounted() {
    this.characterData("alisa");
  },
  methods: {
    upIndex() {
      this.itemCount += 1;
      return this.itemCount;
    },
    setSelected(arg) {
      this.selectedCharacter = arg;
      this.characterData(arg);
    },
    characterData(character) {
      this.loading = true;
      fetch(window.location.href + "json/" + character + ".json")
        .then((res) => res.json())
        .then((dat) => {
          this.bark = dat;
          this.loading = false;
        });
    },
    isItem(input) {
      let isImg = false;
      try {
        require("../assets/" + input + ".svg");
        isImg = true;
      } catch {
        isImg = false;
      }
      return isImg;
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
.item {
  width: 30px;
  height: 30px;
}
.header {
  display: flex;
  width: 100%;
  color: whitesmoke;
}
h1 {
  padding: 2%;
}
.home {
  display: flex;
  flex-wrap: wrap;
  align-content: center;
  justify-content: center;
  height: 86%;
  padding: 1%;
}
.loading {
  display: flex;
  width: 85%;
  color: whitesmoke;
  align-items: center;
  justify-content: center;
  height: 800px;
}
.character {
  padding: 5%;
  margin: 1px;
  background-color: #293037;
  transition: all 0.2s;
  color: whitesmoke;
  text-transform: capitalize;
  border: 2px solid gray;
}
.character:hover {
  background-color: #004f81;
  border-color: #00d9ff;
  box-shadow: 1px 1px 1px 1px #00d9ff;
}
.characters {
  width: 15%;
  background-color: white;
  height: 90%;
  overflow-x: hidden;
  overflow-y: scroll;
}
.moves {
  width: 80%;
  overflow-x: hidden;
  overflow-y: scroll;
  height: 90%;
  border: 2px solid whitesmoke;
  padding-right: 6px;
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
  align-content: center;
  text-align: center;
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
  align-self: center;
}
.inputs {
  width: 40px;
  height: 40px;
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

/* Transition Group Animation Settings */
.list-item {
  display: inline-block;
  margin-right: 10px;
}
.list-enter-active,
.list-leave-active {
  transition: all 1s;
}
.list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
  opacity: 0;
  transform: translateY(30px);
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 10s;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.slide-fade-enter-active {
  transition: all 0.3s ease;
}
.slide-fade-leave-active {
  transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}
.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active below version 2.1.8 */ {
  transform: translateX(10px);
  opacity: 0;
}

.component-fade-enter-active,
.component-fade-leave-active {
  transition: opacity 0.3s ease;
}
.component-fade-enter, .component-fade-leave-to
/* .component-fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
.active {
  background-color: #004f81;
  border-color: #00d9ff;
  box-shadow: 1px 1px 1px 1px #00d9ff;
}
@media only screen and (max-width: 800px) {
  .home {
    padding-top: 5%;
  }
  .characters {
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    height: 25%;
    border: 2px solid lightblue;
    justify-content: space-evenly;
    background-color: #293037;
  }
  .character {
    padding: 1%;
    margin: 1%;
    min-width: fit-content;
    width: 25%;
    text-align: center;
  }
  .moves {
    margin-top: 2%;
    width: 100%;
    height: 75%;
  }
}
</style>