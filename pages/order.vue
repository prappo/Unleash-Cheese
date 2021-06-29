<template>
  <div>
      <section id="order-section">
        <div class="location-container">
            <div class="location">
                <span>your location</span>
                <select>
                    <option>irvine,ca</option>
                    <option>boca,ca</option>
                </select>
            </div>

            <div class="provider-wraper">
            <div class="provider-container">

                <div id="grubhub">
                    <img src="assets/grubhub.png">
                   
                </div>

                <div id="doordash">
                    <img src="assets/doordash.png">
                    
                </div>
            </div>

            <div id="providerBtnContainer">
                <button class="btnProvider">go!</button>
                <button class="btnProvider">go!</button>
            </div>
        </div>
        </div>

        <div class="qoute">
            <h1>cheesed to meet you.</h1>
        </div>
    </section>
  </div>
</template>

<script>
export default {}
</script>

<style scoped>
#order-section{
  height: 150vh;
  background-image: url('/assets/bgorder.png');
  background-size: contain;
  background-repeat: no-repeat;
  background-color: #fff8d6;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.provider-container{
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 30px;
  
  
}

.provider-wraper{
  padding:30px;
  background-color: #FFF8D6;
  border: 8px solid #7C2916;
}

#providerBtnContainer{
  padding-top: 20px;
  display: flex;
  justify-content: space-around;
}

.btnProvider{
  background: #7C2916;
  border:none;
  color: white;
  font-weight: 700;
  font-size: 3rem;
  width: 40%;
  border-radius: 10px;
}

.location{
  padding-bottom: 30px;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 20px;
}


.location span {
  color:#7C2916;
  font-weight: 600;
  font-style: italic;
  font-size: 2rem;
}

.location select{
  background-color: #7C2916;
  color: white;
  border-radius: 10px;
  font-size: 3rem;
  font-weight: 600;
  padding:5px 30px;
}

#grubhub{
  display: flex;
  flex-direction: column;
}

#doordash{
  display: flex;
  flex-direction: column;
}

.qoute{
  margin-top: 20%;
  font-weight: 900;
  color: #7C2916;
  font-size: 3rem;
}


</style>
