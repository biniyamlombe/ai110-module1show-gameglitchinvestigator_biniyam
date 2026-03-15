# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
  When I first ran it, there were several confusing logical errors right away. The game layout immediately looked like I was already missing attempts, and the hint system actively gave me the wrong clues!

- List at least two concrete bugs you noticed at the start:
  1. **Attempt Counter Glitch**
     - **Expected:** The game should give me a full set of attempts (e.g., 0 used) when I load the page.
     - **Actual:** The `attempts` state started at 1, which immediately stole one of my chances to guess before I even started playing.
  2. **Backwards Higher/Lower Hints**
     - **Expected:** If I guess 50 and the secret is 30, the game should say "Too High, Go LOWER!".
     - **Actual:** The code for `check_guess` actually returned "Too High, 📈 Go HIGHER!", purposefully giving mathematically wrong advice to the player.
  3. **Reversed Difficulty Bounds**
     - **Expected:** The "Hard" difficulty should have a wider range of numbers to guess from (like 1 to 100) compared to "Normal" (like 1 to 50).
     - **Actual:** The outputs were swapped in the logic! "Normal" was set to 1 to 100, making it harder than "Hard" mode.

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
