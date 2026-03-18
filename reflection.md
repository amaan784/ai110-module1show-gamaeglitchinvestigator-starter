# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

When I first ran the game it looked like a normal number guessing app, but things started falling apart as soon as I made a few guesses. The hints were completely backwards. If my guess was too high, the game told me to "Go HIGHER!" and if my guess was too low it told me to "Go LOWER!" This sent me in the wrong direction every single time and made it impossible to find the secret number by following the feedback.

The second thing I noticed was that Hard mode was actually easier than Normal mode. Normal mode gives you a range of 1 to 100, but Hard mode only uses 1 to 50. That means you have fewer numbers to guess from on Hard, which makes it simpler, not harder. The difficulty labels did not match the actual challenge at all.

The third bug was that the info message at the top always said "Guess a number between 1 and 100" no matter which difficulty I picked. Even on Easy mode where the real range is 1 to 20, the message still showed 1 to 100. This was confusing because the displayed range did not match the actual range being used behind the scenes.

On top of all that, every even numbered attempt secretly converted the answer to a string before comparing it to my guess. This caused the comparison logic to behave unpredictably because comparing an integer to a string does not work the way you would expect. So sometimes the hints were wrong not just because they were flipped, but because the data types did not even match up correctly.

---

## 2. How did you use AI as a teammate?

I used VS Code Copilot with Opus 4.6 in Agent mode throughout this project to help identify bugs, refactor code, and write tests. It worked like a pair programming partner where I described what I was seeing and it helped trace the problems back to specific lines.

One correct suggestion from the AI was that the hint messages in check_guess were reversed. It pointed out that when guess > secret the code returned "Go HIGHER!" instead of "Go LOWER!" and that swapping the two message strings would fix the problem. I verified this by running pytest with a test that checks whether guessing 75 against a secret of 50 returns a message containing "LOWER," and the test passed after the fix.

One suggestion that was initially misleading was how the AI handled the buggy try/except TypeError block in the original check_guess function. When it refactored the code into logic_utils.py it removed that entire block without explaining why. The original code had a fallback that converted the guess to a string and compared it to the secret as a string, which was there to handle the even attempt type mismatch bug. I had to review the diff carefully to make sure removing it did not break anything, and I confirmed through testing that the simplified version still handles all normal integer comparisons correctly.

---

## 3. Debugging and testing your fixes

I decided a bug was really fixed by writing targeted pytest cases and then running the full test suite to make sure nothing else broke. If the tests passed and the behavior matched what I expected, I considered the fix confirmed. I also used the Developer Debug Info expander in the live app to watch the secret number and compare it against the hints while playing.

One specific test I ran was test_too_high_hint_says_go_lower in test_game_logic.py. It calls check_guess(75, 50) and asserts that the outcome is "Too High" and the message contains the word "LOWER." Before the fix this would have failed because the original message said "Go HIGHER!" instead. After the fix all six tests passed, which told me both the hint logic and the difficulty range were working correctly.

The AI helped me design the tests by generating the initial pytest structure and suggesting that I check the message content, not just the outcome string. That was a good call because the outcome could be "Too High" while the player facing message still said the wrong thing. Checking for "LOWER" inside the message string caught exactly the kind of mismatch that the original bug created.

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
