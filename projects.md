# Projects related to DOM

# Solution code

## project 1 - bg color changer

```javascript

const buttons = document.querySelectorAll('.button')
const body = document.querySelector("body")

buttons.forEach(function(button){
  console.log(button)
  button.addEventListener('click', function(e){
    console.log(e)
    console.log(e.target)
    if(e.target.id === 'grey'){
      body.style.backgroundColor = e.target.id
    }
    if(e.target.id === 'white'){
      body.style.backgroundColor = e.target.id
    }
    if(e.target.id === 'blue'){
      body.style.backgroundColor = e.target.id
    }
    if(e.target.id === 'yellow'){
      body.style.backgroundColor = e.target.id
    }
    if(e.target.id === 'purple'){
      body.style.backgroundColor = e.target.id
    }
  })
});

```

## project 2 - BMI calculator

```javascript

const form = document.querySelector('form')

form.addEventListener('submit', function(e){
  e.preventDefault();

  const height = parseInt(document.querySelector('#height').value)

  const weight = parseInt(document.querySelector('#weight').value)

  const results = document.querySelector('#results')

  if(height === '' || height < 0 || isNaN(height)){
     results.innerHTML = `Please provide valid height ${height}`
  }
  
  else if(weight === '' || weight < 0 || isNaN(weight)){
    results.innerHTML = `Please provide valid weight ${weight}`
 }
 else{
     const bmi = (weight / ((height*height)/10000)).toFixed(2)
     results.innerHTML = `<span>${bmi}</span>`
 }
})

```

## project 3 - Digital clock

```javascript
const clock =  document.getElementById('clock')


setInterval(function(){
  let date = new Date()
//console.log(date.toLocaleTimeString())
clock.innerHTML =  date.toLocaleTimeString()

},1000)

```


## project 4 - Random Number Guess Game 

```javascript
let randomNum = parseInt(Math.random() * 100 + 1);

const submit = document.querySelector('#subt');

const userInput = document.querySelector('#guessField');

const guessSlot = document.querySelector('.guesses');

const remainingSlot = document.querySelector('.lastResult');

const lowORhi = document.querySelector('.lowOrHi')

const startOver = document.querySelector('.resultParas')

const p = document.createElement('p')

let prevGuess = []
let numGuess = 1 
let playGame = true

if(playGame){
     submit.addEventListener('click', function(e){
       e.preventDefault()
       const guess = parseInt(userInput.value)
       validateGuess(guess)
     })
}
function validateGuess(guess){
   if(isNaN(guess)){
     alert('please enter a valid number')
   }
   else if(guess<1){
    alert('please enter a valid number more than 0')
   }
   else if(guess>100){
    alert('please enter a valid number less than 100')
   }
   else{
     prevGuess.push(guess)
     if(numGuess === 11){
       displayGuess(guess)
       displayMessage(`game over. random number was ${randomNum}`)
       endGame()
     }
     else{
       displayGuess(guess)
       checkGuess(guess)
     }
   }
}

function checkGuess(guess){
  if(guess === randomNum){
    displayMessage("You guessed it right.")
    endGame()
  }
  else if(guess < randomNum){
    displayMessage("number is too low")
  }
  else if(guess > randomNum){
    displayMessage("number is too high")
  }
}

function displayGuess(guess){
   userInput.value = ''
   guessSlot.innerHTML += `${guess} `
   numGuess++
   remainingSlot.innerHTML = `${11-numGuess}`
}

function displayMessage(message){
   lowORhi.innerHTML = `<h2>${message}</h2>`
}

function newGame(){
 const newGameBtn = document.querySelector('#newGame')
 newGameBtn.addEventListener('click', function(e){
  randomNum = parseInt(Math.random() * 100 + 1);
  prevGuess = []
  numGuess = 1
  guessSlot.innerHTML = ''
  remainingSlot.innerHTML = `${11 - numGuess}`;
  userInput.removeAttribute('disabled')
  startOver.removeChild(p)

   playGame=true
 })
}

function endGame(){
  userInput.value = ''
  userInput.setAttribute('disabled', '')
  p.classList.add('button')
  p.innerHTML = `<h2 id = "newGame">Start new game</h2>`
  startOver.appendChild(p)
  playGame = false
  newGame();
}
```