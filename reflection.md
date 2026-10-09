# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?

It looked like it was working properly, but when you look into the debuging tool and see that the hints are being given wrong 
and the number of attempts are wrong you notice the first two bugs, and later when you try starting a new game you notice another bug.

- List at least two concrete bugs you noticed at the start  
  (for example: "the hints were backwards").

  Hints were given wrong and the number of attempts the player had are displayed wrong.

**Bug Reproduction Log**

Document at least 3 bugs you found. Add rows as needed.

| Input | Expected Behavior | Actual Behavior | Console Output / Error |
|-------|-------------------|-----------------|------------------------|
| | | | | Attempts be 8     | Attempts are 7  | Line 96

| | | | | Giving High and    | Giving the wrong     |  Line 38
          low hints according| hints not following  |     
          to the secret #    | the secret number    |

| | | | | New game button     | Not restarting the  | Line 134
          restarts the game   | game properly       |
          when pressed        |

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?

Claude and Gemini

- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).

The suggestion to fix this part of the code that hints were being give wrong: def check_guess(guess, secret):
    # Convert both inputs to numbers so comparison works reliably
    try:
        guess_num = float(guess)
        secret_num = float(secret)
    except (ValueError, TypeError):
        return "Error", "⚠️ Invalid input! Please enter a valid number."

    if guess_num == secret_num:
        return "Win", "🎉 Correct!"
    elif guess_num > secret_num:
        return "Too High", "📉 Go LOWER!"
    else:
        return "Too Low", "📈 Go HIGHER!"

- Give one example of an AI suggestion you did not accept as written (including what the AI suggested, why you rejected or changed it, and how you verified your version). It does not have to be a suggestion that was wrong: over-engineered, out of scope, harder to read, or a poor fit for this codebase all count.

It tried to give me this solution for fixing the new game problem, but I got another answer with a much simpler fix so I didn't add this part to my code:
  if new_game:
      st.session_state.attempts = 0
      st.session_state.secret = random.randint(1, 100)
      st.session_state.status = "playing"  # <-- FIX: Reset the game status!
      st.success("New game started.")
      st.rerun()

  if st.session_state.status != "playing":
      if st.session_state.status == "won":
          st.success("You already won. Start a new game to play again.")
      else:
          st.error("Game over. Start a new game to try again.")
      st.stop()

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?

I saved the file and refreshed the game page and tried playing the game and checked if the bug was fixed

- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.

I played the game and gave both higher and lower numbers then the secret number to see if the hints were being given properly after changing the code.

- Did AI help you design or understand any tests? How?

No I didn't run any tests with AI.

---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?

Think of a Streamlit app like a Python script that re-runs completely from top to bottom every time you click a button or change an input.

Because the script restarts every time, standard variables reset to zero. Session State (st.session_state) is Streamlit's memory—it's a persistent dictionary that saves your data (like scores, game status, or guesses) so it isn't wiped out during those script reruns.
---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.

  Instead of sending entire codes that can confuse the AI, just send a section of it so it's more efficient in it's answer.

- What is one thing you would do differently next time you work with AI on a coding task?

  I don't know if there is anything I would do differently to be honest

- In one or two sentences, describe how this project changed the way you think about AI generated code.

It shows how powerful AI is it can go through the code extremely quickly and debug the code faster than any human could because we would have to go from line 1 until we found the issue with the code. 
