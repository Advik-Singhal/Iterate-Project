# Iterate walkthrough

**Advik Singhal · Beyond Prompts**  
Target length: about three minutes.

## Open with the cursor

*On screen: show a cursor and a target if you have a diagram, or open the notebook title.*

“Imagine you’re watching a cursor move towards a target. Suddenly it goes the wrong way. You know it’s a mistake before you say anything. Could a computer pick up a signal from that moment using just three EEG channels?”

“In my Replicate, I averaged EEG responses to faces and objects. This time, I wanted to see what I could learn from individual events and whether the same model would work on a later recording.”

## Show how the test works

*On screen: show the notebook’s design and the first recording’s split.*

“I used two recordings from the same participant, taken 51 days apart. I took the first 600 milliseconds after each cursor move and trained one classifier with 64 channels and another with three. They used the same type of model, time window, and trials. The three channels were Fz, FCz, and Cz, along the front and centre of the scalp.”

“I used the first recording to train both models and decide when they should flag a move as a mistake. Then I tested the frozen models on the later recording.”

## Compare what each model caught

*On screen: show the comparison chart and point to the second recording.*

“With 64 channels, I caught 97 out of 117 errors. With three channels, I caught 69. Balanced accuracy dropped from 87.6 percent to 78.9 percent.”

“Now look at the false alarms. The full model flagged 34 correct moves. The three-channel model flagged five. In this experiment, fewer channels meant fewer interruptions at the thresholds I chose, but also more missed errors.”

*If showing the ROC chart, point to the markers.* “Each marker shows where I set the decision threshold using the first recording. The curves show the trade-off across different thresholds.”

## Close on why it matters

“This was one person watching a cursor. I’d repeat the comparison with the other participants before trying it on a design task.”

“The question I’m working towards is what happens when an AI changes your design and gets a detail wrong. If the AI could learn when to pause and ask, ‘What did I miss?’, that would change how we give it feedback.”
