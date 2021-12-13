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
  name: "HomeComponent",
  created() {
    let options = {
      headers: { "Content-Type": "application/" },
      url: "http://localhost:9000/newGame",
      method: "get",
    };
    let result = axios(options);
  },
};
</script>