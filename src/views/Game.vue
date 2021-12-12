<template>
  <div>
    <div id="uno-GameField">
      <div class="maincontent_Center">
        <div id="gameMessage"></div>
        <div class="maincontent_Left">
          <img
            src="../assets/pics/UNO_Logo.png"
            width="200"
            class="Pic_Center"
            id="unoCall"
            align="Right"
          />
          <img
            src="../assets/pics/cards/Stack.png"
            width="100"
            class="Pic_Center"
            id="pullStack"
          />
        </div>
        <div id="stackCard"></div>
        <br />
        <br />
        <div id="handCard"></div>
      </div>
    </div>

    <div id="wishGame-GameField">
      <div class="maincontent_Center">
        <div id="wishMessage">WishColor!</div>
        <img
          src="../assets/pics/cards/Red_Radio.png"
          width="100"
          class="Pic_Center"
          id="wishRed"
        />
        <img
          src="../assets/pics/cards/Green_Radio.png"
          width="100"
          class="Pic_Center"
          id="wishGreen"
        />
        <img
          src="../assets/pics/cards/Yellow_Radio.png"
          width="100"
          class="Pic_Center"
          id="wishYellow"
        />
        <img
          src="../assets/pics/cards/Blue_Radio.png"
          width="100"
          class="Pic_Center"
          id="wishBlue"
        />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Game",
  components: {},
  data: function () {
    return {
      connection: null,
      playStackCard: "",
      playernameCurrent: "",
      playernameNext: "",
      playerCardsCurrent: [],
      playerCardsNext: [],
      callUno: false,
      wishColor: "",
      wishValue: "",
      index: 0,
    };
  },

  methods: {
    sendMessage: function (message) {
      console.log(this.connection);
      this.connection.send(message);
    },

    setCardPicPath: function (card) {
      var color = "";
      var value = "";
      if (card.includes("red")) {
        color = "Red_";
      } else if (card.includes("blue")) {
        color = "Blue_";
      } else if (card.includes("yellow")) {
        color = "Yellow_";
      } else if (card.includes("green")) {
        color = "Green_";
      } else {
        color = "Black_";
      }
      if (card.includes("<-->")) {
        value = "Reverse.png";
      } else if (card.includes("Ø")) {
        value = "Skip.png";
      } else if (card.includes("4+ ColorSwitch")) {
        value = "4+ColorSwitch.png";
      } else if (card.includes("ColorSwitch")) {
        value = "ColorSwitch.png";
      } else if (card.includes("+2")) {
        value = "+2.png";
      } else if (card.includes("0")) {
        value = "0.png";
      } else if (card.includes("1")) {
        value = "1.png";
      } else if (card.includes("2")) {
        value = "2.png";
      } else if (card.includes("3")) {
        value = "3.png";
      } else if (card.includes("4")) {
        value = "4.png";
      } else if (card.includes("5")) {
        value = "5.png";
      } else if (card.includes("6")) {
        value = "6.png";
      } else if (card.includes("7")) {
        value = "7.png";
      } else if (card.includes("8")) {
        value = "8.png";
      } else if (card.includes("9")) {
        value = "9.png";
      } else {
        value = "Radio.png";
      }
      return color + value;
    },
    updateGame: function () {
      var ref = this;
      this.callUno = false;
      let index = 0;

      $("#uno-GameField").css("visibility", "visible");
      $("#wishGame-GameField").css("visibility", "collapse");
      $("#unoCall").attr("src", require("@/assets/pics/UNO_Logo.png"));
      $("#gameMessage").empty();
      $("#gameMessage").append(
        "<h4>PLAYER " + this.playernameCurrent + " it´s your turn</h4>"
      );
      $("#stackCard").empty();

      $("#stackCard").append(
        '<img class="img-fluid handCards" src="' +
          require("@/assets/pics/cards/" +
            ref.setCardPicPath(ref.playStackCard)) +
          '" width="100" id= "PlayStack">'
      );
      $("#handCard").empty();
      this.playerCardsCurrent.forEach((handcard) => {
        if (handcard.includes("black")) {
          $("#handCard").append(
            '<img class="img-fluid handCards" src="' +
              require("@/assets/pics/cards/" + ref.setCardPicPath(handcard)) +
              '" width="100" id= ' +
              index +
              ">"
          );
          document.getElementById(index).addEventListener("click", function () {
            ref.setBlackCard(index);
          });
        } else {
          $("#handCard").append(
            '<img class="img-fluid handCards" src="' +
              require("@/assets/pics/cards/" + ref.setCardPicPath(handcard)) +
              '" width="100" id= ' +
              index +
              ">"
          );
          document.getElementById(index).addEventListener("click", function () {
            ref.setCard(index);
          });
        }
        index = index + 1;
      });

      if (this.wishColor != "") {
        this.wishColor = "";
        this.wishValue = "";
        location.reload();
      }
      this.index = index;
    },

    setBlackCard: async function (cardIndex) {
      $("#uno-GameField").empty();
      $("#wishGame-GameField").css("visibility", "visible");
      this.wishValue = cardIndex;
    },

    setWishColor: async function (color) {
      this.wishColor = color;
      this.setCard(this.wishValue + " " + this.wishColor);
    },

    setCard: async function (cardIndex) {
      var ref = this;
      let json = "";
      console.log(cardIndex);
      if (ref.callUno === false) {
        json = JSON.stringify({
          set: {
            cardIndex: cardIndex,
          },
        });
      } else {
        json = JSON.stringify({
          call: {
            cardIndex: cardIndex,
          },
        });
      }
      let options = {
        headers: { "Content-Type": "application/json" },
        url: "http://localhost:9000/set",
        method: "get",
        data: json,
      };
      console.log(json);
      let result = await axios(options);
      const {
        playStackCard,
        playernameCurrent,
        playernameNext,
        playerCardsCurrent,
        playerCardsNext,
      } = result;
      ref.updateGame;
      alert("Passt");
    },

    getCard: async function () {
      var ref = this;
      let json = "";
      json = JSON.stringify({
        get: {},
      });
      let options = {
        headers: { "Content-Type": "application/json" },
        url: "http://localhost:9000/get",
        method: "get",
        data: json,
      };
      console.log(json);
      let result = await axios(options);
      const {
        playStackCard,
        playernameCurrent,
        playernameNext,
        playerCardsCurrent,
        playerCardsNext,
      } = result;
      ref.updateGame;
    },
  },
  created() {
    var ref = this;
    console.log("Starting connection to UNO-WebSocket Server");
    this.connection = new WebSocket("ws://localhost:9000/websocket");
    this.connection.onopen = function (event) {
      //console.log(event)
      console.log("Successfully connected to Stratego Websocket Server");
    };
    this.connection.onclose = function () {
      console.log(
        "Successfully closed connection to Stratego Websocket Server"
      );
    };
    this.connection.onerror = function (error) {
      console.log("Error occured in Stratego Websocket Server: " + error);
    };
    this.connection.onmessage = function (e) {
      if (typeof e.data === "string") {
        console.log(e.data);
        //let unofield = new UnoField;
        let result = JSON.parse(e.data);
        ref.playStackCard = result.game.playStackCard;
        ref.playernameCurrent = result.game.playerListNameCurrent;
        ref.playerCardsCurrent = result.game.playerListCardsCurrent;

        ref.playernameNext = result.game.playerListNameNext;
        ref.playerCardsNext = result.game.playerListCardsNext;
        ref.updateGame();
      }
    };
  },

  mounted() {
    var ref = this;
    document.getElementById("unoCall").addEventListener("click", function () {
      if (this.callUno === true) {
        this.callUno = false;
        let imgSrc = require("@/assets/pics/UNO_Logo.png");
        $("#unoCall").attr("src", imgSrc);
      } else {
        this.callUno = true;
        let imgSrc = require("@/assets/pics/CallUno.png");
        $("#unoCall").attr("src", imgSrc);
      }
    });

    document.getElementById("pullStack").addEventListener("click", function () {
      ref.getCard();
    });

    document.getElementById("wishRed").addEventListener("click", function () {
        ref.setWishColor('red')
    });
    document.getElementById("wishGreen").addEventListener("click", function () {
        ref.setWishColor('green')
    });
    document.getElementById("wishYellow").addEventListener("click", function () {
        ref.setWishColor('yellow')
    });
    document.getElementById("wishBlue").addEventListener("click", function () {
        ref.setWishColor('blue')
    });
  },
};
</script>