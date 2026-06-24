# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- List at least two concrete bugs you noticed at the start  
  (for example: "the hints were backwards").
  -when click new game and change difficulty the attempt numbers changes for all the difficulties and the easy has lower attemps than the normal.
  -when i click the new game button after playing a game, the new game does not start
  -score does not correctly count score and after last attempt score sometimes shows and other times does not
  -hints are backwards of target
  -easy, normal and difficult have the same range of 1 to 100 despite them needing to be different ranges; also the secret range stays between 1-100

**Bug Reproduction Log**

Document at least 3 bugs you found. Add rows as needed.

| Input | Expected Behavior | Actual Behavior | Console Output / Error |
|---20----|-go high (target 91)--|go low-|--none---|
|10| -go high (target 91)|go low| none|
|---50----|-go high (target 91)--|go low-|--none---|
|---60----|-go high (target 91)--|go low-|--none---|
|last attempt|display correct score(-30)|display incorrect score(-35)|--none---|
|last attempt|display correct score(-35)|did not display score|--none---|
|50-60-70-80-90-100-101|go lower and stop attempt higher than 100|did opposite said go low and let me attemp 101|none|
|last attempt|display correct score(0)also not counting score after each attempt|display incorrect score(-5)|--none---|
## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).

I used copilot.
-One suggestion was that the start button does not restart the status, score or history. i verified the result during my testing of the game and also reviewing the section of the code that details the start new game feature and it was correct it only restarted attemps and secret but not the status , score or history.I entered the code for the missing resets and verified the that it worked by testing in the game. For this i wrote my own code and just took the information of the logic from AI.

- another suggestion was that the onscreen prompt did not changes for each difficulty. So i first wrote code to try and fix the issue. however since i am not super familiar with the sintax of python I highlighted the section i wrote and and showed it to copilot and it corrected the synax.i tested this by running the game a checking if it would change based on difficulty..
what i wrote:
st.info():
if difficulty == "Easy":
    f"Guess a number between 1 and 20. Attempts left: {attempt_limit - st.session_state.attempts}"
elif difficulty == "Hard":
    f"Guess a number between 1 and 50. Attempts left: {attempt_limit - st.session_state.attempts}"
else:
    f"Guess a number between 1 and 100. Attempts left: {attempt_limit - st.session_state.attempts}"


co pilot suggested:
if difficulty == "Easy":
    message = f"Guess a number between 1 and 20. Attempts left: {attempt_limit - st.session_state.attempts}"
elif difficulty == "Hard":
    message = f"Guess a number between 1 and 50. Attempts left: {attempt_limit - st.session_state.attempts}"
else:
    message = f"Guess a number between 1 and 100. Attempts left: {attempt_limit - st.session_state.attempts}"

st.info(message)

- i also used Ai to confirm where i though the glitch was. while reading the code i started questioning why the guess had to be changed to a string and not stay an int. the Ai then removed the parsing. i double checked the code by testing it with the game and also reviewing the code again to double check whether there were any other instances of strings where parsing the guess into a string would be nessicary.  

-one example of incorrect suggestion by the AI is that it told me to switch the return values for the following code. Which i did just to see if it would correct the hint messages on the game. (it did) However, the code itself then made no logical sense so I switched it back and read the code to see if there was another code that was attributing to this incorrect output. 

try:
        if guess > secret:
            return "Too Low", "📉 Go LOWER!"
       
        else:
           return "Too High", "📈 Go HIGHER!" 
---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?

I would test out the game and use the developer debug info as a guide. For example for testing the incorrect lower/higher hint glitch i would check whether i put even or odd numbers higher or lower than the target that i would recieve the correct hint.
Ai did give me a hint that the even numbers produced the wrong hint which made me test that before correcting the code. i also ran pytest and it showed as 4 items as passed.

---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?

I would explain streamlit reruns and session state as snapshot of your code when you run the program. if you make any changes to your code you would then need to rerun stream lit to create a new session with your new code.
---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.

one habit i would reuse from this project is reading the code then asking the AI to explain the logic and then rereading the code to confirm if the logic the AI explained is correct. this made it much easier to pick out gliches or things i thought were strange (like changing guess into string)

One Thing i would do differently I work with Ai is that i will make sure to write code before asking AI about that section of code. one thing I noticed is if i asked it about a specific code that i thought was wrong and wished to ask the logic of it; the AI would immediately try to solve it for me. which defeats the purpose of me thinking through it.

This project made me change the way i think about AI generated code by making me think of it as a tentative collaborator. It can be useful to point you in the right direction but it can also try to do the thinking for you so you have to propt it well to not fall in that trap.
