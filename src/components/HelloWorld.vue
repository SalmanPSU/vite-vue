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

  <div class="btn-wrapper">
    <button id="duplicate">Duplicate</button>
    <button id="delcard">Delete card</button>
    <button id="background">Toggle background color</button>
    <button id="heading">Change heading</button>
  </div>


  <div class="cards">

    <section class="card" id="arrivals">
      <div class="card-info">
        <h2 id="arrival-heading">New Arrivals</h2>
        <img src="https://media.istockphoto.com/id/482948743/photo/blank-white-t-shirt-front-with-clipping-path.jpg?s=612x612&w=0&k=20&c=cJG_B0mOIG42FKtC_rqIeZCClYOj7UCFNNs9WTkYEEE=">
        <div class="btn-wrapper">
          <button id="details1">Details</button>
        </div>
        <p id="p1">These t-shirts have just arrived!</p>
        </div>
    </section>

    <section class="card">
      <div class="card-info">
        <h2>Deals</h2>
        <img src="https://img.freepik.com/premium-vector/stock-clearance-sale-banner-design_1588-914.jpg?w=2000">
        <div class="btn-wrapper">
          <button id="details2">Details</button>
        </div>
        <p id="p2">We have 70% off on football jerseys!</p>
      </div>
    </section>

    <section class="card">
      <div class="card-info">
        <h2>FAQ</h2>
        <img src="https://cdn.pixabay.com/photo/2015/11/03/08/56/question-mark-1019820_1280.jpg">
        <div class="btn-wrapper">
          <button id="details3">Details</button>
        </div>
        <p id="p3">We have your questions answered!</p>
      </div>
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

.btn-wrapper {
  margin: 24px auto;
}

.btn-wrapper button {
  margin-left: 8px;
  margin-right: 8px;
  font-family: Monospace;
  font-size: 16px;
  color: blue;
  background-color: white;
  transition: transform 0.3s;
}

.btn-wrapper button:hover,
.btn-wrapper button:focus {
  font-size: 16px;
  color: white;
  background-color: #008aff;
  transform: scale(1.2);
}

.cards {
  display: flex;
  max-width: 8000px;
  margin: auto;
  justify-content: center;
}

.card {
  max-width: 250px;
  background-color: gray;
  border: 1px solid black;
  margin: 16px;
  padding: 16px;
  display: flex;
  flex-direction: column;
  align-items: center;
  transition: transform 0.3s;
}

.remove-bg {
  background-color: white;
}

.card img {
  width: 250px;
  height: 250px;
  border-radius: 8px;
}

.card-info {
  text-align: center;
  margin-top: 8px;
}

@media (max-width: 799px) {
  .btn-wrapper {
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
    const newArrivalsDetails = document.querySelector('#details1');
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
    const dealsDetails = document.querySelector('#details2');
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
    const faqDetails = document.querySelector('#details3');
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

    //Scale card on hover
    const allCards = document.querySelectorAll('.card'); 

    allCards.forEach(function(card) {           
        card.addEventListener('mouseenter', function() {
            card.style.backgroundColor = '#008aff';
        });

        card.addEventListener('mouseleave', function() {
            card.style.backgroundColor = '';
        });
    });
  }
}
</script>