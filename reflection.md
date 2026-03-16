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
  I primarily used the integrated AI assistant (Gemini) and Claude Code throughout this project to help debug logic errors, understand Streamlit's session state, and develop my Pytest tests.
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
  The AI correctly identified that Streamlit reruns the entire script on every user interaction (like clicking a button), which is why my secret number kept changing. It suggested using `st.session_state` to store `secret_number` and `attempts` so they persist across reruns. I verified this by implementing the session state checks, and the game immediately started keeping the same secret number for the entire round.
- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).
  When I was trying to figure out why the "Too High/Too Low" hints were backwards, the AI initially suggested I just swap the inequality signs (`>` and `<`) in the `app.py` UI file. However, I checked the `logic_utils.py` file myself and realized the core logical flaw was actually in the `check_guess` function where the strings returned were swapped, so changing the UI wouldn't have actually fixed the underlying logic flaw.

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
  I verified fixes by running the Streamlit app locally and manually playing through the game to ensure the logic behaved correctly (e.g., the secret number didn't reset and hints were accurate). I also relied on the pytest suite passing successfully to confirm my changes didn't break core logic.
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
  I ran pytest on the game logic functions to test specific scenarios, such as guessing 50 when the secret is 30. This automated test immediately showed me that the strings returned by the high/low hint logic were reversed, isolating the bug to `logic_utils.py` without me needing to click through the game UI repeatedly.
- Did AI help you design or understand any tests? How?
  Yes, the AI helped explain how to use pytest assertions effectively. It also guided me on the importance of separating the core game logic from the Streamlit UI code so that the logic functions could be tested independently.

---

## 4. What did you learn about Streamlit and state?

- In your own words, explain why the secret number kept changing in the original app.
  The secret number kept changing because Streamlit is designed to re-run the entire script from top to bottom every time the user interacts with the app (like pressing the "Submit Guess" button). Without saving the number, the script simply picked a new random number every time it ran.
- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
  Imagine a chef cooking a meal from scratch every time you ask for a sip of water. That's a Streamlit "rerun"—it builds the entire page from the ground up every time you blink. "Session state" is like giving the chef a notepad so they remember they already cooked the main course, allowing them to just focus on giving you the water.
- What change did you make that finally gave the game a stable secret number?
  I used `st.session_state` to check if a `secret_number` already existed. If it didn't (`if "secret_number" not in st.session_state`), I generated and saved one. By pulling the number from the session state instead of generating it fresh, the number stayed exactly the same across reruns.

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.
