<br>
#### CV
# Vera Karmanovich
#### Junior front-end developer
<hr>
#### CONTACTS
* Location: Pinsk, Belarus <br>
* Phone: +375-29-59-64-187 <br>
* Telegram: @Ba_Reum <br>
* e-mail: bareum.dev@gmail.com <br>
* GitHub: <code>[bareum-dev](https://github.com/bareum-dev)</code> <br>
<hr>

#### PROFILE
I'm beginner Front-End developer.  
I love to create beautiful things with my hands and I use JavaScript for this.


#### SKILLS
* HTML
* CSS
* JavaScript
* Node.js Basic
* Pug
* SASS/SCSS
* BEM
* Git, GitHub

#### EDUCATION
Moscow Institute of Enterpreneurship and Law (MIPP) - B.A. Economics  
2007-2012

#### LANGUAGES
Russian - Native
English - A2-B1

#### CODE EXAMPLE
```javascript
let inputs = document.querySelectorAll('.input');
let startGame = document.querySelector("#start-game");
let resetBtn = document.querySelector("#reset-btn");
let infoBlock = document.querySelector('#info-block');

let usedCities = [];
let usersPoints = [0, 0];

// start game btn
startGame.addEventListener('click', function startGameFn(e) {
  infoBlock.innerHTML = "";

  usedCities = [];
  console.log(usedCities);

  startGame.removeEventListener('click', startGameFn);
  startGame.setAttribute('disabled', 'true');

  inputs[0].removeAttribute('disabled');
  inputs[0].focus();

  inputs[0].removeAttribute("placeholder");
  inputs[1].removeAttribute("placeholder");
  
  let startGameMessage = document.createElement('p');
  startGameMessage.textContent = "the game has begun";
  infoBlock.prepend(startGameMessage);

  for (let input of inputs) {
    input.addEventListener('keypress', inputCityName)
  }

  resetBtn.addEventListener("click", () => {
    usedCities = [];
    usersPoints = [0, 0];

    infoBlock.innerHTML = '';
    infoBlock.textContent = "the game has been reset";

    startGame.addEventListener("click", startGameFn);
    startGame.removeAttribute("disabled");

    inputs[0].setAttribute("disabled", 'true');
    inputs[1].setAttribute("disabled", 'true');

    inputs[0].setAttribute("placeholder", "press start game");
    inputs[1].setAttribute("placeholder", "press start game");
  });
});


// get name of city
function inputCityName(e) {
  let valueOfActiveInput = inputs[0].value || inputs[1].value;
  let indexOfInput = !(inputs[0].hasAttribute('disabled')) ? 0 : 1;

  if (e.key == 'Enter') {
    // is array 'usedCities' empty?
    if (usedCities.length == 0) {
      usedCities.push(valueOfActiveInput.toLowerCase());
      console.log(usedCities);

      // message
      let par = document.createElement("p");
      par.textContent = `${valueOfActiveInput}`;
      infoBlock.prepend(par);
      if (indexOfInput == 0) {
        par.classList.add("text-player-one");
      } else {
        par.classList.add("text-player-two");
      }

      // add point
      if (indexOfInput == 0) {
        usersPoints[0] += 1;
      } else {
        usersPoints[1] += 1;
      }
      console.log(usersPoints);

      // change input
      for (let input of inputs) {
        if (input.hasAttribute("disabled")) {
          input.removeAttribute("disabled");
          input.focus();
        } else {
          input.setAttribute("disabled", "true");
          input.value = "";
        }
      }
    }

    // if array 'usedCities' isn't empty
    if (
      usedCities.length > 0 
      &&
      usedCities[usedCities.length - 1]
        .endsWith(valueOfActiveInput.slice(0, 1).toLowerCase())
      &&
      !usedCities.includes(valueOfActiveInput)
      &&
      valueOfActiveInput != ''
    ) {
      // add city to 'usedCities' array
      usedCities.push(valueOfActiveInput);
      console.log(usedCities);

      // message
      let par = document.createElement("p");
      par.textContent = `${valueOfActiveInput}`;
      infoBlock.prepend(par);
      if (indexOfInput == 0) {
        par.classList.add("text-player-one");
      } else {
        par.classList.add("text-player-two");
      }

      // add point
      if (indexOfInput == 0) {
        usersPoints[0] += 1;
      } else {
        usersPoints[1] += 1;
      }
      console.log(usersPoints);

      // change input
      for (let input of inputs) {
        if (input.hasAttribute("disabled")) {
          input.removeAttribute("disabled");
          input.focus();
        } else {
          input.setAttribute("disabled", "true");
          input.value = "";
        }
      }
    }
    else if (usedCities > 0 && usedCities.includes(valueOfActiveInput)) {
      let doubleCityName = document.createElement("p");
      doubleCityName.textContent = `${valueOfActiveInput} has already been used`;
      infoBlock.prepend(doubleCityName);
    }
    else if (
      !(usedCities[usedCities.length - 1]
        .endsWith(valueOfActiveInput.slice(0, 1).toLowerCase()))
    ) {
      let lastLetter = usedCities[usedCities.length - 1].slice(-1);
      console.log(lastLetter);
      let wrongCityName = document.createElement("p");
      wrongCityName.textContent = `name of a city must begin with the letter "${lastLetter}"`;
      infoBlock.prepend(wrongCityName);
    }

    // is input.value empty?
    if (valueOfActiveInput == "") {
      let emptyStringMessage = document.createElement("p");
      emptyStringMessage.textContent = "enter a name of a city";
      infoBlock.prepend(emptyStringMessage);
    }
  }
}

```