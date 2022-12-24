<template>
  <div id="container">
    <div class="text-container">
      <div class="uv">
        <img src="@/assets/icons/uv-index.png" alt="">
        <p>{{Math.trunc(uvInfo.uv)}}</p>
      </div>
      <div class="stats">
        <img height="20px" src="@/assets/icons/up.png" alt="">
        <caption>{{Math.trunc(uvInfo.uv_max)}}</caption>
        <img height="20px" src="@/assets/icons/clock.png" alt="">
        <caption>{{ maxTime }}</caption>
      </div>
    </div>
    <svg
        style="enable-background:new 0 0 50 50;" version="1.1"
        viewBox="0 0 50 50"
        x="0px"
        xml:space="preserve"
        xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        y="0px">
      <circle id="sunBeam" cx="25" cy="25" r="20">
        <animate attributeName="opacity" dur="3s" from="1" repeatCount="indefinite" to="0"/>
        <animate
            attributeName="r"
            attributeType="XML"
            begin="0s"
            dur="3s"
            fill="remove"
            from="12"
            repeatCount="indefinite"
            to="20"
        />
      </circle>
      <circle id="sun" cx="25" cy="25" r="13"/>
    </svg>
<!--    Max today: {{ uvResult.result.uv_max }}-->
<!--    Max at:{{ uvResult.result.uv_max_time }}-->
<!--    Max time: {{ uvResult.result.safe_exposure_time.st4 }}minutes-->
  </div>
</template>

<script>
export default {
  name: "SunIcon",
  props: {
    uvInfo: {
      type: Object,
      default: () => {}
    }
  },
  computed: {
    maxTime: function() {
      const date = new Date(this.uvInfo.uv_max_time)
      return  `${date.getHours()}:${date.getMinutes()}`
    }
  }
}
</script>

<style scoped>
#container {
  width: 500px;
  height: 400px;
  display: flex;
  justify-content: center;
  align-items: center;
}

#sun {
  fill: #ffe160;
}

#sunBeam {
  fill: #ffe160;
  stroke: #fbeC5d;
  stroke-width: 3;
  stroke-linecap: round;
}

.text-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  position: absolute;
}

.text-container caption, .text-container p {
  font-family: Helvetica, 'Helvetica Neue', sans-serif;
  color: floralwhite;
  font-weight: 700;

}
.uv {
  margin-top: -90px;
}
.uv p {
  animation: bounce 1.5s ease infinite alternate;
  font-size: 4rem;
  margin-top: 90px;
  margin-left: 12px;
  /*border: 1px solid white;*/
}

.text-container .stats, .uv {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
}

.text-container caption {
  font-size: 1rem;
  margin-top: 5px;
}

.stats {
  margin-top: -70px;
  margin-right: -10px;
}

.stats caption {
  margin-right: 10px;
}




/*p {*/
/*  color: #EEE;*/
/*  padding-top: 30px;*/
/*  font-family: 'Coiny', cursive;*/
/*  text-align: center;*/
/*  font-size: 70px;*/
/*}*/

@keyframes bounce {
  0% {
    transform:scale(.9);
  }
  20% {
    transform:scale(1);
  }
}

</style>