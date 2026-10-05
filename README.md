# 🎮 Game Glitch Investigator: The Impossible Guesser

## 🚨 The Situation

You asked an AI to build a simple "Number Guessing Game" using Streamlit.
It wrote the code, ran away, and now the game is unplayable. 

- You can't win.
- The hints lie to you.
- The secret number seems to have commitment issues.

## 🛠️ Setup

1. Install dependencies: `pip install -r requirements.txt`
2. Run the broken app: `python -m streamlit run app.py`

## 🕵️‍♂️ Your Mission

1. **Play the game.** Open the "Developer Debug Info" tab in the app to see the secret number. Try to win.
2. **Find the State Bug.** Why does the secret number change every time you click "Submit"? Ask ChatGPT: *"How do I keep a variable from resetting in Streamlit when I click a button?"*
3. **Fix the Logic.** The hints ("Higher/Lower") are wrong. Fix them.
4. **Refactor & Test.** - Move the logic into `logic_utils.py`.
   - Run `pytest` in your terminal.
   - Keep fixing until all tests pass!

## 📝 Document Your Experience

- [ ] Describe the game's purpose.
A number-guessing game built by AI with hidden bugs. The goal is to find and fix them, using AI and tests.
- [ ] Detail which bugs you found.
The hints were backwards, the secret was turned into a string on even attempts, and New Game ignored the difficulty range.
- [ ] Explain what fixes you applied.
I swapped the hint messages and removed the string conversion. I also moved the logic into logic_utils.py and added tests, which all pass but 'The New Game' range is still broken.

## 📸 Demo Walkthrough

## Demo Walkthrough

Sample game on Normal difficulty (range 1–100, 8 attempts). The secret number is 50.

1. The game starts with a score of 0. The player enters **40**.
2. The game shows **"📈 Go HIGHER!"** (outcome: Too Low). The score drops by 5, to **-5**.
3. The player enters **70**. The game shows **"📉 Go LOWER!"** (outcome: Too High). The score drops by 5, to **-10**.
4. The player enters **60**. The game shows **"📉 Go LOWER!"** again. The score rises by 5, to **-5**.
5. The player enters **abc**. The game shows **"That is not a number."** and the score stays at **-5**.
6. The player enters **50**. The game shows **"🎉 Correct!"**, plays balloons, and reports **"You won! The secret was 50."** The win adds 40 points, for a final score of **35**.
7. The game is over. Any further guess shows "You already won. Start a new game to play again."


## 🧪 Test Results

```
# configfile: pytest.ini
testpaths: tests
plugins: anyio-4.15.1
collected 5 items                                                                                                                                                                                       

tests\test_game_logic.py .....                                                                                                                                                                    [100%]

========================================================================================== 5 passed in 0.02s ===========================================================================================
```

## 🚀 Stretch Features

- [ ] [If you choose to complete Challenge 4, describe the Enhanced UI changes here — a screenshot is optional]
