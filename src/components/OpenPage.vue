<template>
    <div id="open-page">
        <div class="main-title animate__animated animate__backInDown">את"ת מנוע וממסרת</div>
        <div id="sub-title">היום תתרגלו ותבחנו על איתור ותפעול תקלות במנוע ובממסרת, ענו על השאלות וקבלו ציון ומשוב</div>
        <button @click="nextPage" class="start-btn">בואו נתחיל </button>
    </div>
</template>



<script>
export default {
    name: 'open-page',
    props: [],
    data() {
        return {
            
        }
    },
    methods: {
        nextPage() {
            this.$emit('next-page');
        }
    }
}
</script>

<style scoped>

#open-page {
    margin: 0%;
    height: 100%;
    width: 100vw;
    position: absolute;
    top: 0;
    right: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    z-index: 2;
}
.main-title {
    text-align: center;
    color:rgb(255, 255, 255);
    font-family: "RubikDood";
    /* font-weight: bold; */
    font-size: 13vw;
    
    margin: 2%;
    margin-top: 40%;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
}
#sub-title {
    text-align: center;
    color:rgb(255, 255, 255);
    /* font-family: "Huninn"; */
    font-weight: 500;
    font-size: 6.5vw;
    margin: 2%;
    margin-top: 10%;
    text-shadow: 2px 4px 4px rgba(0, 0, 0, 0.3);
}

.start-btn {
    position:relative;
    overflow:hidden;
    padding:16px 42px;
    border:none;
    border-radius:14px;
   background: #d5b08e;
    color:white;
    font-size:20px;
    font-weight:bold;
    cursor:pointer;
    border: 1px solid #a1480d;
    animation: pulse 1.6s infinite;
}


.start-btn::before{
    content:"";
    position:absolute;
    top:0;
    left:-120%;
    width:70%;
    height:100%;
    background:linear-gradient(
        120deg,
        transparent,
        rgba(255,255,255,.6),
        transparent
    );
    transition:.7s;
}

.start-btn:hover::before{
    left:150%;
}

@keyframes pulse {

  0% {
    transform: scale(1);
    box-shadow: 0 6px 12px rgba(0,0,0,.25);
  }

  50% {
    transform: scale(1.08);
    box-shadow: 0 10px 22px rgba(185,125,87,.55);
  }

  100% {
    transform: scale(1);
    box-shadow: 0 6px 12px rgba(0,0,0,.25);
  }

}
</style>