# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?
When I first ran the game, it looked like a normal number guessing game with a title, difficulty dropdown, text input, and buttons. Everything seemed fine on the surface until I actually started playing.

Three bugs I noticed right away:
The hints were backwards. When I guessed too high, the game told me to go higher, sending me in the completely wrong direction.
The attempts counter was lying. It would show "Attempts left: 1" but then immediately say "Out of attempts!" on the same screen, so I never got to use that last turn.
The info message always said "Guess a number between 1 and 100" even when I picked Easy, which contradicted the sidebar showing "Range: 1 to 20."

---

## 2. How did you use AI as a teammate?

I used Claude Code as my AI tool for this project. I used it to refactor code across multiple files, fix bugs, and generate tests.
Correct AI suggestion: After playing the game and noticing the hints were sending me in the wrong direction, I prompted Claude Code to fix the backwards hint messages in check_guess. It correctly swapped the messages so that "Too High" now says "Go LOWER!" and "Too Low" says "Go HIGHER!" I verified this by running the game and guessing a number I knew was too high. The hint now correctly told me to go lower. I also wrote pytest cases that check the hint text, and all tests passed.
Incorrect/misleading AI suggestion: When I asked Claude Code to review the difficulty settings, it flagged the Hard mode range (1 to 50) as a bug, saying Hard should have the widest range since it is the hardest level. But when I looked at it more carefully, I realized Hard gives you only 5 attempts for 50 numbers, while Normal gives 8 attempts for 100 numbers. That actually makes Hard harder. The smaller range is a design choice, not a bug. The AI jumped to a conclusion based on the numbers looking out of order without considering the attempt limits.

---

## 3. Debugging and testing your fixes
I decided a bug was fixed by checking it two ways: running automated tests with pytest and then manually playing the game. If both gave me the right behavior, I was confident the fix worked. Just seeing the code change wasn't enough — I needed to see it actually work.
For the hints bug, I ran five pytest cases in tests/test_game_logic.py. Two of them specifically targeted my fix: one checked that guessing 60 against a secret of 50 returns a message containing "LOWER," and the other checked that guessing 40 against 50 returns a message containing "HIGHER." All five tests passed, which told me the hint messages were now pointing in the correct direction. I also ran the game with streamlit run app.py, guessed a number I knew was too high, and confirmed the hint told me to go lower.
Claude Code helped me design the tests. I described the bug I fixed and asked it to generate pytest cases that verify the hint direction. It wrote the tests and also fixed the existing starter tests, which were broken because they compared against a string instead of unpacking the tuple that check_guess returns. I would not have caught that issue with the starter tests on my own without running them first.

---

## 4. What did you learn about Streamlit and state?

Streamlit works differently from a regular app. Every time you click a button or interact with anything, the entire script runs again from top to bottom. That means if you store a variable like secret = 5 normally, it gets reset to a new value on every click. Session state is how you get around that. It is like a storage box that Streamlit keeps aside and does not wipe between reruns. So instead of secret = 5, you write st.session_state.secret = 5, and it remembers the value even when the page reruns. If I were explaining it to a friend, I would say: imagine every time you press a button, the whole page reloads from scratch, but session state is a sticky note on the side that survives each reload.

---

## 5. Looking ahead: your developer habits

One habit I want to reuse is writing small, focused commits after each fix instead of doing everything in one big commit at the end. During this project I committed after the refactor, after the hint fix, after the attempts fix, and after the tests. That made it easy to track what changed and why, and if something broke, I could trace it back to a specific commit.
Next time I work with AI on a coding task, I would not take every suggestion at face value. In this project, the AI flagged the Hard difficulty range as a bug, but when I thought about it myself, it was actually a valid design choice. That taught me to always verify AI suggestions against the actual behavior instead of just accepting them.
This project changed the way I think about AI generated code. It showed me that AI can write code that looks clean and complete on the surface but still has real logic bugs hiding underneath. The code ran without errors, but the game was basically unplayable until I tested it myself.
