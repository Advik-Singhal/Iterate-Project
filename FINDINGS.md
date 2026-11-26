# Findings

How much performance does a cursor error classifier lose when it relies on three EEG channels? On the second recording from participant 1 in BNCI2015-013, balanced accuracy fell from **87.6% with 64 channels to 78.9% with three**. Both versions used the same event windows, features, classifier settings, and evaluation trials. All fitting and threshold selection used the first recording.

| Test recording | Input | Balanced accuracy | Errors caught | False alarms |
| --- | --- | ---: | ---: | ---: |
| First, blocks 9 and 10 | 64 channels | 82.0% | 14/18 | 10/73 |
| First, blocks 9 and 10 | Three channels | 75.0% | 9/18 | 0/73 |
| First, blocks 9 and 10 | Always predict correct | 50.0% | 0/18 | 0/73 |
| Later, all 10 blocks | 64 channels | 87.6% | 97/117 | 34/438 |
| Later, all 10 blocks | Three channels | 78.9% | 69/117 | 5/438 |
| Later, all 10 blocks | Always predict correct | 50.0% | 0/117 | 0/438 |

## What the results show

- **Fewer channels.** Three channels reduced balanced accuracy by 8.7 percentage points on the later recording. A paired bootstrap that resampled whole recording blocks estimated a 95% interval of a **4.6 to 12.6 point drop** within that recording.
- **Later recording.** Both versions scored above the 50% baseline on the recording 51 days later. They also scored higher than on the two first-day test blocks. That comparison uses different numbers of blocks and trials, so the higher later scores cannot establish an improvement over time.
- **False alarms.** On the later recording, the 64-channel model caught 82.9% of errors and raised 7.8 false alarms per 100 correct moves. The three-channel model caught 59.0% and raised 1.1 per 100. Each model had its own threshold, chosen with the same rule and a 10% false-alarm target on the validation blocks. The target does not guarantee the same false-alarm rate on either test split.

## Checks across thresholds and movement directions

I used the original locked model scores for this follow-up check. The later recording's ROC AUC was **0.940 with 64 channels** and **0.892 with three**. AUC measures how often an incorrect move scores higher than a correct one, with ties counted as half. The [ROC figure](recording-2-roc.svg) shows the trade-off across thresholds and marks the operating points fixed on the first recording.

The full model also had higher AUC when I compared errors and correct moves within each movement direction. This suggests that the difference persists beyond simply distinguishing leftward from rightward movement. Direction alone leaves other features of the visual task, such as target location and expectations, unresolved.

| Movement | Errors | Correct moves | 64-channel AUC | Three-channel AUC |
| --- | ---: | ---: | ---: | ---: |
| Leftward | 74 | 210 | 0.952 | 0.903 |
| Rightward | 43 | 228 | 0.920 | 0.870 |

## Scope and next step

This is an offline result from one participant in a controlled cursor task with known movement times. The three selected signals came from a laboratory EEG cap. A three-electrode device could have different signal quality and referencing. The next test would repeat this protocol with the other dataset participants, then use the results to design a separate task around noticing interface edits.

[Executed notebook](iterate_executed.ipynb) · [Machine-readable results](results.json) · [Source protocol](https://lampx.tugraz.at/~bci/database/013-2015/description.pdf)
