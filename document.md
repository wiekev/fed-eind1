function createCaroCarrousel(carrouselID) {
  let carrousel = document.querySelector("#"+carrouselID);
  let carrouselElementsContainer = carrousel.querySelector(":scope > ul");
  let carrouselElements = carrouselElementsContainer.querySelectorAll("section:nth-of-type(4) article ul li");

  let linkButtons = carrousel.querySelectorAll(":scope > section:nth-of-type(4) article > a");




function iniLinkButtons() {    
    for(linkButton of linkButtons) {
			// beide link-buttins naar kliks laten luisteren
      linkButton.addEventListener("click", function(e){
        // als er geklikt wordt
				// de default-actie (de link volgen) niet uitvoeren
				e.preventDefault();

				// bepalen of er op 'previous' of 'next' geklikt is
				let direction = this.getAttribute("href");
				// naar het element gaan
				goToElement(direction);
      });
    }
	}

function iniStartPosition() {
        // eerste element current maken
        carrouselElements[0].classList.add("current");
        // eerste bolletje current maken
            bolletjes[0].classList.add("current");
            // aan het begin van de container starten
        carrouselElementsContainer.scrollLeft = 0;
      }    



      function goToElement(direction) {
		// het huidige current element opzoeken
		let currentElement = carrousel.querySelector(":scope > section:nth-of-type(4) article ul > .current");

		let newElement;
		if (direction == "previous") {
			// het nieuwe element is het vorige broertje/zusje
			newElement = currentElement.previousElementSibling;
			// checken of nieuwe element bestaat - anders naar laatste
			if (!newElement) {
				newElement = carrousel.querySelector(":scope > section:nth-of-type(4) article ul > li");
			}
		} else {
			// het nieuwe element is het volgende broertje/zusje
			newElement = currentElement.nextElementSibling;
			// checken of nieuwe element bestaat - anders naar eerste
			if (!newElement) {
				newElement = carrousel.querySelector(":scope > section:nth-of-type(4) article ul > li");
			}
		}

		// naar het nieuwe element scrollen
		scrollToElement(newElement);
  }
        
  function scrollToElement(newElement) {
    // carousel container opzoeken
    let carouselElementsContainer = newElement.closest("ul");

		// de linker offset van het nieuwe element bepalen 
		let newElementOffset = newElement.offsetLeft;
		
		// de carousel naar de berekende positie scrollen
		carouselElementsContainer.scrollTo({
			left: newElementOffset
		});
    
    // nieuwe element current element maken
    updateCurrentElement(newElement);

    // de bolletjes updaten
    updateBolletjes(newElement);
  }
    

  function updateCurrentElement(newElement) {
    // het huidige current element opzoeken
    let currentElement = carrousel.querySelector(":scope > ul > .current");
    // de class current verwijderen
    currentElement.classList.remove("current");

    // aan nieuwe element de class current toevoegen
    newElement.classList.add("current");
}



// de linkbuttons activeren
iniLinkButtons();	
// de carrousel bij het begin starten
iniStartPosition();
}

(function() {
    // hier de id gebruiken van de section in de html
    createCaroCarrousel("bolletjesAndLinkButtons");
    //je kunt hier ook meerdere carrousellen activeren
  })();







  section:nth-of-type(4) article ul{
  margin: 0;
  padding: 0;
  list-style: none;
  display: flex;
  overflow: hidden;
  scroll-snap-type: inline mandatory;
  scroll-behavior: smooth;
  -webkit-overflow-scrolling: touch;
}

section:nth-of-type(4) article ul::-webkit-scrollbar{
  display: none;
}

section:nth-of-type(4) article ul li{
  flex-basis: 100%;
  flex-shrink: 0;
  scroll-snap-align: center;
}

section:nth-of-type(4) > ul li > img{
  width: 100%;
  /* margin: 2em;
  border-radius: 2em; */
  display: block;
}


section:nth-of-type(4) article > a{
  position: absolute;
  width: 3em;
  aspect-ratio: 1/1;
  top: calc(50% - 1.5em);
  color: green;
  background-color: pink;
  outline: none;
  box-shadow: inset 0 0 0 1px black;
  display: grid;
  place-items: center;
  transition: 0.5s;
}

section:nth-of-type(4) article > a[herf="vorige"] {
  left: -3.5em;
}

section:nth-of-type(4) article > a[herf="volgende"] {
  right: -3.5em;
}

section:nth-of-type(4) article:hover > a[href="previous"],
section:nth-of-type(4) article:focus-within > a[href="previous"] {
  left:.5em;
}
section:nth-of-type(4) article:hover > a[href="next"],
section:nth-of-type(4) article:focus-within > a[href="next"] {
  right:.5em;
}

section:nth-of-type(4) article > a::before, section:nth-of-type(4) article > a::after {
  content: "";
  position: absolute;
  width: 1em;
  height: 4px;
  background: red;
}

section:nth-of-type(4) article > a[href=previous]::before {
	transform-origin: 2px center;
	transform: translateY(0) rotate(45deg);
}
section:nth-of-type(4) article > a[href=previous]::after {
	transform-origin: 2px center;
	transform: translateY(0) rotate(-45deg);
}

section:nth-of-type(4) article > a[href=next]::before {
	transform-origin: calc(100% - 2px) center;
	transform: translateY(0) rotate(45deg);
}
section:nth-of-type(4) article > a[href=next]::after {
	transform-origin: calc(100% - 2px) center;
	transform: translateY(0) rotate(-45deg);
}

section:nth-of-type(4) article > a:hover,
section:nth-of-type(4) article > a:focus {
  color: orange;
}