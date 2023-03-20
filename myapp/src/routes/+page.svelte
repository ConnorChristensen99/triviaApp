<script>
  import { append_empty_stylesheet } from "svelte/internal";


    let difficulties = [
        {id: 'easy', text: 'Easy'},
        {id: 'medium', text: 'Medium'},
        {id: 'hard', text: 'Hard'},
    ]

    let categories = [
      {id: 27, text: 'Animals'},
        {id: 25, text: 'Art'},
        {id: 20, text: 'Mythology'}
    ]

    let styles = [
        {id: 'multiple', text: 'Multiple Choice'},
        {id: 'boolean', text: 'True/False'},

    ]

    let diffSelected;
    let catSelected;
    let styleSelected;
    let answer ='';
    let correctTotal = 0;








    //Scores the game and ends it
    function scoreGame() {
      let body = document.getElementById('body')
      let div = document.createElement('div')
      div.style.cssText = 'background-color: #83b2b9; height: 200px; width: 300px; z-index: 100; padding: 2%; display: flex; justify-content: center; align-items: center; margin-top: 2%; border: 1px solid black;'

      
      let DOMQuestions = document.getElementById('questions')
      DOMQuestions.style.cssText = 'display: none;'
      body.style.cssText = 'display: display;'

        for(let i=1; i <= 10; i++) {
        let answer = document.querySelector(`#indivID${i} .answer`)
        let answer4 = document.querySelector(`#indivID${i} #selected`)


        if(answer.innerText == answer4.innerText) {
          correctTotal += 1
        }
      }

      let totalText = document.createElement('span')
      totalText.style.cssText = 'color: white;'
      totalText.textContent = `You got ${correctTotal} out of 10 right!`
      totalText.style.cssText = 'font-size: x-large; color: black;'

      div.append(totalText)
      body.append(div)

    }



//STUPID I AM ASHAMED OF HOW I DID THIS BUT IM SO TIRED
//STUPID I AM ASHAMED OF HOW I DID THIS BUT IM SO TIRED
//STUPID I AM ASHAMED OF HOW I DID THIS BUT IM SO TIRED
//STUPID I AM ASHAMED OF HOW I DID THIS BUT IM SO TIRED
    function addStylingAnswer(answer, incAnswer1, incAnswer2, incAnswer3) {
      answer.style.cssText = 'border: 4px solid green; padding: 2%; width: 80%; margin: 2%;'
      answer.setAttribute('id', 'selected')
      incAnswer1.style.cssText = 'padding: 2%; width: 80%; margin: 2%;'
      incAnswer1.removeAttribute('#selected')
      incAnswer2.style.cssText = 'padding: 2%; width: 80%; margin: 2%;'
      incAnswer2.removeAttribute('#selected')
      incAnswer3.style.cssText = 'padding: 2%; width: 80%; margin: 2%;'
      incAnswer3.removeAttribute('#selected')
    }
    function addStylingincAnswer1(answer, incAnswer1, incAnswer2, incAnswer3) {
      answer.style.cssText = 'padding: 2%; width: 80%; margin: 2%;'
      answer.removeAttribute('#selected')
      incAnswer1.style.cssText = 'border: 4px solid green; padding: 2%; width: 80%; margin: 2%;'
      incAnswer1.setAttribute('id', 'selected')
      incAnswer2.style.cssText = 'padding: 2%; width: 80%; margin: 2%;'
      incAnswer2.removeAttribute('#selected')
      incAnswer3.style.cssText = 'padding: 2%; width: 80%; margin: 2%;'
      incAnswer3.removeAttribute('#selected')
    }
    function addStylingincAnswer2(answer, incAnswer1, incAnswer2, incAnswer3) {
      answer.style.cssText = 'padding: 2%; width: 80%; margin: 2%;'
      answer.removeAttribute('#selected')
      incAnswer1.style.cssText = 'padding: 2%; width: 80%; margin: 2%;'
      incAnswer1.removeAttribute('#selected')
      incAnswer2.style.cssText = 'border: 4px solid green; padding: 2%; width: 80%; margin: 2%;'
      incAnswer2.setAttribute('id', 'selected')
      incAnswer3.style.cssText = 'padding: 2%; width: 80%; margin: 2%;'
      incAnswer3.removeAttribute('#selected')
    }
    function addStylingincAnswer3(answer, incAnswer1, incAnswer2, incAnswer3) {
      answer.style.cssText = 'padding: 2%; width: 80%; margin: 2%;'
      answer.removeAttribute('#selected')
      incAnswer1.style.cssText = 'padding: 2%; width: 80%; margin: 2%;'
      incAnswer1.removeAttribute('#selected')
      incAnswer2.style.cssText = 'padding: 2%; width: 80%; margin: 2%;'
      incAnswer2.removeAttribute('#selected')
      incAnswer3.style.cssText = 'border: 4px solid green; padding: 2%; width: 80%; margin: 2%;'
      incAnswer3.setAttribute('id', 'selected')
    }
//STUPID I AM ASHAMED OF HOW I DID THIS BUT IM SO TIRED
//STUPID I AM ASHAMED OF HOW I DID THIS BUT IM SO TIRED





    //Closes the test
    function closeTest() {
      body.style.cssText = 'display: display;'

      let DOMQuestions = document.getElementById('questions')
      DOMQuestions.style.cssText = 'display: none;'
    }





    //Pulls questions when play
    async function handlePlay() {

      let body = document.getElementById('body')
      body.style.cssText = 'display: none;'

      let DOMQuestions = document.getElementById('questions')
      DOMQuestions.style.cssText = 'display: display;'
      DOMQuestions.textContent = ""

      let count = 1


      //Creating button to close test
      const close = document.createElement('button')
      close.innerText = "Close Test"
      close.style.cssText = 'float: right; font-size: large; color: red;'
      close.addEventListener('click', function(){ closeTest();})
      DOMQuestions.append(close)


        let difficulty = diffSelected.id
        let category = catSelected.id
        let style = styleSelected.id





        //Fetching questions
        const response = await fetch(`https://opentdb.com/api.php?amount=10&category=${category}&difficulty=${difficulty}&type=${style}`);
        const data = await response.json()

        let questions = data.results











        //Displaying questions
        questions.forEach(question => {

          let divQuestion = document.createElement('div')
          divQuestion.setAttribute('id', `indivID${count}`)
          divQuestion.style.cssText = 'background-color: grey; padding: 5%; display: flex; justify-content: center; flex-direction: column; margin: 30px;'

          let indivQuestion = document.createElement('li')
          indivQuestion.textContent = count + ". " + question.question
          indivQuestion.style.cssText='font-size: x-large;'
          divQuestion.append(indivQuestion)





          //Creating the individual answer items and hooking them to determine if they are correct //DUMB DUMB DUMB DUMB
          let answer = document.createElement('button')
          answer.addEventListener('click', function(){addStylingAnswer(answer, incAnswer1, incAnswer2, incAnswer3);})
          answer.setAttribute('id', 'answer')
          answer.style.cssText='padding: 2%; width: 80%; margin: 2%;'

          let incAnswer1 = document.createElement('button')
          incAnswer1.setAttribute('id', 'incorrect1')
          incAnswer1.addEventListener('click', function(){addStylingincAnswer1(answer, incAnswer1, incAnswer2, incAnswer3);})
          incAnswer1.style.cssText='padding: 2%; width: 80%; margin: 2%;'

          let incAnswer2 = document.createElement('button')
          incAnswer2.setAttribute('id', 'incorrect2')
          incAnswer2.addEventListener('click', function(){addStylingincAnswer2(answer, incAnswer1, incAnswer2, incAnswer3);})
          incAnswer2.style.cssText='padding: 2%; width: 80%; margin: 2%;'

          let incAnswer3 = document.createElement('button')
          incAnswer3.setAttribute('id', 'incorrect3')
          incAnswer3.addEventListener('click', function(){addStylingincAnswer3(answer, incAnswer1, incAnswer2, incAnswer3);})
          incAnswer3.style.cssText='padding: 2%; width: 80%; margin: 2%;'




          answer.textContent = question.correct_answer
          answer.setAttribute('class', 'answer')
          incAnswer1.textContent = question.incorrect_answers[0]
          incAnswer2.textContent = question.incorrect_answers[1]
          incAnswer3.textContent = question.incorrect_answers[2]

          
         
          divQuestion.append(incAnswer1)
          divQuestion.append(incAnswer2)
          divQuestion.append(answer)
          divQuestion.append(incAnswer3)
          

         let DOMQuestions = document.getElementById('questions')

         DOMQuestions.append(divQuestion)

         count +=1
        });

        let submitButton = document.createElement('button')
        submitButton.textContent = 'Submit'
        submitButton.addEventListener('click', function(){scoreGame()})
        submitButton.style.cssText='background: linear-gradient(90deg, rgba(2,0,36,1) 0%, rgba(29,121,9,1) 0%, rgba(0,212,255,1) 100%); border: none; height: 50px; width: 200px; border-radius: 10px; font-size: large; float: right; cursor: pointer;'

        DOMQuestions.append(submitButton)
    }


</script>






<div id="body">

<h1>Trivia App</h1>

<div id='setup'>

  <h3>Setup Game</h3>
<form on:submit|preventDefault={handlePlay}>
	<select bind:value={diffSelected} on:change="{() => answer = ''}">
		{#each difficulties as difficulty}
			<option value={difficulty}>
				{difficulty.text}
			</option>
		{/each}
	</select>

    <select bind:value={catSelected} on:change="{() => answer = ''}">
		{#each categories as category}
			<option value={category}>
				{category.text}
			</option>
		{/each}
	</select>

    <select bind:value={styleSelected} on:change="{() => answer = ''}">
		{#each styles as style}
			<option value={style}>
				{style.text}
			</option>
		{/each}
	</select>

	<button class="submitButton" type=submit>
		Play!
	</button>
</form>
</div>
</div>
<div id="questionz">
<ul id="questions">

</ul>
</div>




<style>
  #body {
    flex-direction: column;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  #questions {
    max-width: 700px;
    list-style-type: none;
  }
  #questionz {
    display: flex;
    justify-content: center;
  }
  .submitButton {
    background: linear-gradient(90deg, rgba(2,0,36,1) 0%, rgba(29,121,9,1) 0%, rgba(0,212,255,1) 100%);
    border: none;
    height: 50px;
    width: 200px;
    border-radius: 10px;
    font-size: large;
  }
  .submitButton:hover {
    cursor: pointer;
    background: #1d7909;
    color: white;
  }
  select {
    padding: 1%;
    margin: 2%;
  }
  #setup {
    background-color: gray;
    padding: 3%;
  }
  .addedClass {
    border: 1px solid green;
    background-color: rgba(2,0,36,.3)
  }
</style>








