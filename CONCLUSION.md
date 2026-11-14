# Lab 05 — Conclusion

<!--
Read this before you write.

This file is graded by your instructor, by hand, and it is worth 6 of the 15 points.

- Type it yourself. Do not use a chatbot, an AI assistant, an AI autocomplete or a "rewrite my
  text" tool for any part of it, not even for grammar. English that is plain and a little
  clumsy but yours is better than polished text that is not.
- Use your own numbers. Every number you quote must be one your own notebook printed. Copy
  the number exactly as it appeared. A number your notebook did not print is marked as wrong.
- Answer in your own words, about 80-200 words per question. A short answer that uses your
  numbers beats a long answer that could have been written by anyone.
- Delete these comment lines if you like. Keep the three headings and the last line.
-->

## 1. Which layer changed your results the most?

Give the numbers before -> after for that layer (correct / wrong / no answer, out of 20) and say
whether it changed what the agent *can do* or only what it *admits*. If no layer changed the
number of correct answers, say so and explain what the layers did change instead.

(write here)
Layer 1 changed the results the most. The bare agent got 16/24 correct, 4 wrong, and 4 no answers. After Layer 1, the results improved to 18/24 correct, 6 wrong, and 0 no answers. This layer helped the agent recover from tool errors instead of stopping immediately. Layer 2 did not change the number of correct answers: it remained 18/24. Layer 3 also kept the number of correct answers at 18/24, but it changed some wrong answers into no answers by checking whether numbers were grounded in tool outputs. After adding notes, the agent reached 19/24 correct. Overall, the layers improved reliability, but they could not guarantee that the model used the correct formula.

## 2. One failure the full harness did not fix

Pick one question that the full harness (layer 3) still gets wrong or refuses. Give its id
(q01 ... q20). Open its trace in the notebook: at which step did it go wrong, and what did
the model do instead? Name one thing you would add to the harness, and what it would cost
(extra model calls, tokens, time, or a new way to fail).

(write here)
The full harness still got q17 wrong. The agent retrieved the correct unemployment rates for Aktobe: 4.5% in 2020 and 4.1% in 2023. However, it used a relative percentage change formula instead of calculating the difference in percentage points. It returned 8.89 instead of the correct answer, 0.4 percentage points. Layer 3 accepted the answer because 8.89 appeared in the calculator tool output. This shows that grounding checks where a number came from, but not whether the calculation matches the question. I would add a unit-aware validation step to distinguish percentage changes from percentage-point differences. This would require extra validation logic and possibly another model call, increasing execution time and token usage.

## 3. Workflow or agent for the monthly ranking?

Dala Insight wants to publish, every month, "which region is highest and which is lowest on one
indicator in one year". Would you ship the fixed workflow or the agent? Use the accuracy, the
number of model calls, the tokens and the time you measured in Part 1. Then say in one sentence
what kind of question would make you choose the other one.

(write here)
I would choose the fixed workflow for the monthly ranking because the question has a known structure: finding the highest and lowest regions for one indicator in one year. On the 15 fixed-shape questions, the workflow got 13/15 correct, while the bare agent got 9/15 correct. The workflow used 15 model calls, 3,852 tokens, and 16.2 seconds. The agent used 26 model calls, 19,835 tokens, and 52.6 seconds. Therefore, the workflow was more accurate, used fewer tokens and calls, and was faster. I would choose the agent for open-ended questions that do not fit a predefined workflow.

---

I wrote this file myself, without any AI tool.
