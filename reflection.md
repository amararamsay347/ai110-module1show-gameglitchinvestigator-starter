# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- List at least two concrete bugs you noticed at the start  
  (for example: "the hints were backwards").

  The game was confusing at first since I used normal mode and did not check the correct answer, entering values like floats, ints, negative numbers, edge cases, and strings as well. The first answer was 19, when entering values larger than 19, was prompted to 'go higher' while values less than 19 were treated as 'go lower'. So one bug was that the hints were backwards, this bug lives in the app.py file in the function check_guess (lines 32 to 47). The other bug was that the sample size shrunk as I proceeded to the hard level, it went from 100 to 50 but the answer that I was given in the hard one was 100, so the sample space was never really reduced to 1 - 50. In the harder level I expected an answer between 1-50 but that was not the case. The error is in app.py line 136, it does not differentiate the modes to reduce or increase the sample size. 

**Bug Reproduction Log**

Document at least 3 bugs you found. Add rows as needed.

| Input | Expected Behavior | Actual Behavior | Console Output / Error |
|-------|-------------------|-----------------|------------------------|
| 55    |GO lower           |Go higher        |none                    |
| 0     |Go higher          |Go lower         |none                    |
| 1     |Go higher          |Go lower         |none                    |

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
- Give one example of an AI suggestion you did not accept as written (including what the AI suggested, why you rejected or changed it, and how you verified your version). It does not have to be a suggestion that was wrong: over-engineered, out of scope, harder to read, or a poor fit for this codebase all count.

Claude was used, I used it to determine that app.py converted the secret to a string on even attempts before calling check_guess which raised a TypeError because it is comparing an int to a string. I also made sure that Claude changed the Go Higher and Go lower hints to match in check_guess, they were also checked with the pytest. One thing claude did that I did not spefically ask for was the addition of the pytest.ini file, I asked the ways to run the pytest and was given a new file. 
---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?

In the streamlit app, I noticed it was fixed since the hints were in their correct flows in the logic_utils.py file. For this, I re-ran the streamlit app and also ran pytests to verify the changes. One pytest that I ran was def test_guess_too_low():
    # If secret is 50 and guess is 40, hint should be "Too Low"
    result = check_guess(40, 50)
    assert result[0] == "Too Low"
This pytest showed me that the check_guess classified the guess below the secret as "Too low". The three tests failed at first becayse check_guess returns a tuple hence, comparing the whole result to a string would never be true and made the three tests wrong. It was fixed to include assert result[0] == "Too Low". 
Yes, Claude helped with explaining why the original tests failed and wrote two regression tests, which would have caught the hint message and the outcome hence why those passed at first.  
---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.
