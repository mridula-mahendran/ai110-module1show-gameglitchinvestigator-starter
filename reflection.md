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

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?

---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.
