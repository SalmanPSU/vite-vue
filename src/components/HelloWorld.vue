<script setup>
import { ref } from 'vue'

defineProps({
  msg: String,
})

const count = ref(0)
</script>

<template>
  <div class="title">
    <h1>Clothing Store</h1>
  </div>

  <div class="button">
    <button id="duplicate">Duplicate</button>
    <button id="delcard">Delete card</button>
    <button id="background">Toggle background color</button>
    <button id="heading">Change heading</button>
  </div>


  <div class="cards">

    <section class="card" id="arrivals">
        <h2 id="arrival-heading">New Arrivals</h2>
        <img src="https://cdn.pixabay.com/photo/2016/03/25/09/04/t-shirt-1278404_1280.jpg" alt="new arrivals">
        <div class="button">
          <button id="dtl1">Details</button>
        </div>
        <p id="p1">We have new t-shirts!</p>
      </section>

    <section class="card" id="deals">
        <h2>Deals</h2>
        <img src="https://img.freepik.com/premium-vector/stock-clearance-sale-banner-design_1588-914.jpg?w=2000">
        <div class="button">
          <button id="dtl2">Details</button>
        </div>
        <p id="p2">We have 70% off on football jerseys!</p>
    </section>

    <section class="card" id="faqs">
        <h2>FAQs</h2>
        <img src="https://cdn.pixabay.com/photo/2015/11/03/08/56/question-mark-1019820_1280.jpg">
        <div class="button">
          <button id="dtl3">Details</button>
        </div>
        <p id="p3">Frequently Asked Questions!</p>
    </section>

  </div>
</template>

<style scoped>
body {
  font-family: Arial, sans-serif;
  text-align: center;
}

.title {
  background-color: #9dcc8b;
  color: black;
  padding: 16px;
}

h1 {
  font-size: 32px;
  margin-bottom: 16px;
}

.button {
  margin: 24px auto;
}

.button button {
  margin-left: 8px;
  margin-right: 8px;
  font-family: Monospace;
  font-size: 16px;
  color: black;
  background-color: white;
  transition: transform 0.3s;
}

.button button:hover,
.button button:focus {
  font-size: 16px;
  color: white;
  background-color: #9dcc8b;
  transform: scale(1.2);
}

.cards {
  display: flex;
  max-width: 8000px;
  margin: auto;
  justify-content: center;
}

.card {
  max-width: 300px;
  background-color: #9dcc8b;
  border: 1px solid black;
  margin: 16px;
  padding: 16px;
  display: flex;
  flex-direction: column;
  align-items: center;
  transition: transform 0.3s;
}


.card img {
  width: 275px;
  height: 300px;
  border-radius: 10px;
}

.remove-bg {
  background-color: white;
}

@media (max-width: 800px) {
  .button {
    display: none;
  }
}
</style>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  mounted() {
    //Duplicate Card
    const arrivalCard = document.querySelector('#arrivals')
    const duplicateButton = document.querySelector('#duplicate')
    const allCardClones = [];

    duplicateButton.addEventListener('click', function() {
        const cardClone = arrivalCard.cloneNode(true);
        arrivalCard.insertAdjacentElement('afterend', cardClone);
        allCardClones.push(cardClone);
    });

    //Delete Card
    const deleteButton = document.querySelector('#delcard')

    deleteButton.addEventListener('click', function() {
        if (allCardClones.length > 0) {
          const lastClonedCard = allCardClones.pop();
          lastClonedCard.remove();
        }
    });

    //Toggle background color
    const backgroundButton = document.querySelector('#background')

    backgroundButton.addEventListener('click', function() {
        if (arrivalCard.classList.contains('remove-bg')) {
          arrivalCard.classList.remove('remove-bg');    
        }
        else {
          arrivalCard.classList.add('remove-bg');      
        }
    });

    //Change heading
    const cardHeading = document.querySelector('#arrival-heading')
    const headingButton = document.querySelector('#heading');
    const originalContent = cardHeading.textContent;
    let textChanged = false;

    headingButton.addEventListener('click', function() {
        if (textChanged) {
            cardHeading.textContent = originalContent;
            textChanged = false;
        } else {
            cardHeading.textContent = 'something else';
            textChanged = true;
        }
    });

    //New Arrivals Details
    const newArrivalsDetails = document.querySelector('#dtl1');
    const newArrivalsParagraph = document.querySelector('#p1');
    let isHidden1 = true;
    newArrivalsParagraph.style.display = 'none'; //hide by default

    newArrivalsDetails.addEventListener('click', function() {
        if (isHidden1) {
            newArrivalsParagraph.style.display = 'block';
            isHidden1 = false;
        } else {
            newArrivalsParagraph.style.display = 'none';
            isHidden1 = true;
        }
    });

    //Deals Details
    const dealsDetails = document.querySelector('#dtl2');
    const dealsParagraph = document.querySelector('#p2');
    let isHidden2 = true;
    dealsParagraph.style.display = 'none'; //hide by default

    dealsDetails.addEventListener('click', function() {
        if (isHidden2) {
            dealsParagraph.style.display = 'block';
            isHidden2 = false;
        } else {
            dealsParagraph.style.display = 'none';
            isHidden2 = true;
        }
    });

    //FAQ Details
    const faqDetails = document.querySelector('#dtl3');
    const faqParagraph = document.querySelector('#p3');
    let isHidden3 = true;
    faqParagraph.style.display = 'none'; //hide by default

    faqDetails.addEventListener('click', function() {
        if (isHidden3) {
            faqParagraph.style.display = 'block';
            isHidden3 = false;
        } else {
            faqParagraph.style.display = 'none';
            isHidden3 = true;
        }
    });
  }
}
</script>