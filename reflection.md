# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

When the game first ran, it was completely glitched out with several intertwined logical errors. The layout falsely consumed an attempt immediately, the initial difficulty bounds were hardcoded backwards (so "Normal" had a larger range than "Hard"), and the "Higher / Lower" hint feedback gave mathematically backward advice. Additionally, out-of-bounds guesses unfairly consumed player attempts, and restarting the game failed to truly clear the user's timeline state. 

---

## 2. How did you use AI as a teammate?

I used an AI coding agent pair-programmer directly within my environment to actively debug the Streamlit application. A great example of a correct AI suggestion was identifying the `except TypeError` block deeply nested in the game mechanics that was unexpectedly type-casting the secret integers to strings and causing lexicographical string sorting failures (e.g. comparing `"10" < "5"`). However, the AI briefly struggled when writing the raw offline `pytest` scripts, as it wrote an assertion assuming the game should output `"Go LOWER!"` when mathematically trying to test a higher number, requiring us to dynamically go back and correct the test's strict equality checks.

---

## 3. Debugging and testing your fixes

We decided that a bug was definitively fixed not by just looking at the code, but by building and passing an offline unit test for each step before committing it individually. For example, `test_new_game_reset()` was a test suite that forcefully mutated the game state, clicked the "New Game" UI button, and mathematically asserted using `AppTest` that the session variables successfully flushed to `[]` and `0`. The AI heavily assisted in designing these test suites, as it drafted the complex `AppTest` fixture logic to interact with Streamlit DOM elements offline.

---

## 4. What did you learn about Streamlit and state?

The initial app kept dropping variables because Streamlit operates on an aggressive top-to-bottom re-execution model; fundamentally, every time a user triggers an input element on the front-end, Streamlit natively rebuilds the entire file from line 1 and destroys arbitrary local memory. I would explain Streamlit "reruns" to a friend like refreshing your web browser over and over—unless you explicitly save data in a special continuous "backpack" (`st.session_state`), it's gone upon refresh. We were able to firmly anchor the secret numbers and attempt limits by securely storing and mutating them only inside `st.session_state`, and directly injecting `st.rerun()` calls to flush the UI cleanly.

---

## 5. Looking ahead: your developer habits

One technical habit I definitely intend to retain is adopting the "step-by-step patch and offline test" pattern, separating changes into distinct focused commits rather than blindly applying 5 fixes at once. In the future when working with AI, I intend to always mentally verify its generated structural equality tests instead of blinding trusting that the AI math logic lines perfectly map to human expectations. Ultimately, this module shifted my paradigm of AI-generated code from being a "perfect finished product" to being a "powerful but fundamentally flawed first draft" that requires a human engineer to securely finalize.
