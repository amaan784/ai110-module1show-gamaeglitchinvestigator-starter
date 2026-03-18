# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

When I first ran the game it looked like a normal number guessing app, but things started falling apart as soon as I made a few guesses. The hints were completely backwards. If my guess was too high, the game told me to "Go HIGHER!" and if my guess was too low it told me to "Go LOWER!" This sent me in the wrong direction every single time and made it impossible to find the secret number by following the feedback.

The second thing I noticed was that Hard mode was actually easier than Normal mode. Normal mode gives you a range of 1 to 100, but Hard mode only uses 1 to 50. That means you have fewer numbers to guess from on Hard, which makes it simpler, not harder. The difficulty labels did not match the actual challenge at all.

The third bug was that the info message at the top always said "Guess a number between 1 and 100" no matter which difficulty I picked. Even on Easy mode where the real range is 1 to 20, the message still showed 1 to 100. This was confusing because the displayed range did not match the actual range being used behind the scenes.

On top of all that, every even numbered attempt secretly converted the answer to a string before comparing it to my guess. This caused the comparison logic to behave unpredictably because comparing an integer to a string does not work the way you would expect. So sometimes the hints were wrong not just because they were flipped, but because the data types did not even match up correctly.

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?

---

## 4. What did you learn about Streamlit and state?

- In your own words, explain why the secret number kept changing in the original app.
- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
- What change did you make that finally gave the game a stable secret number?

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.
