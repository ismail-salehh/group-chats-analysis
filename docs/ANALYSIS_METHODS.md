# Analysis Methods & Mathematical Definitions

This document details the formulas, algorithms, input fields, edge cases, and limitations of every metric calculated in Group Chat Analyzer.

Our core design principle:
> **Distinguish observed facts from inferred approximations.**
>
> We report measurable facts ("Alice sent 31.4% of messages") rather than making unsupported psychological claims ("Alice is the group leader"). Any metric involving heuristic assumptions is explicitly labeled as approximate.

---

## 1. Overview Metrics

### Total Messages
- **Definition**: Total count of message records in the merged conversation.
- **Type**: Observed Fact.
- **Formula**: $N = \text{length}(\text{messages})$
- **Edge cases**: Unsent messages and system notifications are counted in total records, but distinguished in composition breakdowns.

### Active Days
- **Definition**: The count of distinct calendar dates on which at least one message was recorded.
- **Type**: Observed Fact.
- **Formula**: $\text{Count}(\text{Distinct}(\text{YYYY-MM-DD}(\text{timestamp\_ms})))$
- **Timezone**: Evaluated using local client timezone.

### Messages per Active Day
- **Definition**: Message volume normalized against the days the group actually spoke.
- **Type**: Observed Fact.
- **Formula**: $\frac{\text{totalMessages}}{\text{activeDaysCount}}$
- **Limitations**: Much more informative than total messages divided by total calendar days for groups that had hiatuses or seasonal activity.

### Median Message Length
- **Definition**: The statistical median number of word tokens in textual messages.
- **Type**: Observed Fact.
- **Formula**: Middle value of sorted word counts per text message.
- **Why Median**: Unlike mean/average, median is robust against long copy-pasted articles or walls of text skewing the metric.

---

## 2. Participant Script Breakdown

### Script Character Classification
- **Definition**: The distribution of characters in each member's messages categorized by Unicode script family.
- **Type**: Observed Fact.
- **Categories**:
  - **Arabic**: Matches Unicode blocks `[\u0600-\u06FF\u0750-\u077F\u08A0-\u08FF\uFB50-\uFDFF\uFE70-\uFEFE]`.
  - **Latin**: Matches `[A-Za-z\u00C0-\u024F]`.
  - **Digits**: Arabic and Western digits `[0-9\u0660-\u0669]`.
  - **Emojis**: Unicode Extended Pictographic sequences (`\p{Extended_Pictographic}`).
  - **Other / Symbols**: Punctuation and miscellaneous symbols.
- **Formula**: $(\frac{\text{chars\_in\_category}}{\text{total\_non\_whitespace\_chars}}) \times 100$

---

## 3. Conversation Sessions & Bursts

### Session Boundary
- **Definition**: A continuous period of conversational interaction separated by an inactivity threshold.
- **Type**: Operational Heuristic.
- **Default Threshold**: 60 minutes.
- **Rule**: If $\text{timestamp}[i] - \text{timestamp}[i-1] > 60\text{ minutes}$, start a new session burst.
- **Limitations**: A session might contain multiple side topics, or conversely, a slow asynchronous conversation might span across multiple detected bursts.

### Conversation Starters
- **Definition**: The sender of the first message of each detected session burst.
- **Type**: Operational Approximation.
- **Formula**: $\frac{\text{Count}(\text{sessions where starter} == \text{participant})}{\text{totalSessions}}$
- **Limitations**: Initiating an activity burst indicates active messaging cadence, but does not prove social dominance or intentional meeting organization.

---

## 4. Response Time Analysis

### Approximate Response Delay
- **Definition**: The elapsed time between consecutive messages from different participants up to a 6-hour threshold.
- **Type**: Inferred Approximation.
- **Algorithm**:
  For message $B$ from sender $Y$ directly following message $A$ from sender $X$:
  - Condition: $X \ne Y$ and $\text{timestamp}(B) - \text{timestamp}(A) \le 6\text{ hours}$.
  - Delay: $\text{timestamp}(B) - \text{timestamp}(A)$.
- **Distribution Buckets**:
  - `< 1 min` (Immediate reaction / synchronous chat)
  - `1 – 5 mins` (Quick response)
  - `5 – 15 mins` (Short delay)
  - `15 – 60 mins` (Casual check-in)
  - `1 – 6 hours` (Asynchronous return)
- **Limitations**: Group chats do not have guaranteed 1-to-1 reply threading without explicit platform reply metadata. Message $B$ may be a completely independent thought rather than a direct reply to message $A$.

---

## 5. Interaction Network & Transition Matrix

### Transition Edge
- **Definition**: Frequency of consecutive messages between distinct participants within a 15-minute window.
- **Type**: Inferred Approximation.
- **Algorithm**:
  When participant $B$ sends a message within 15 minutes of participant $A$, increment directed edge $A \to B$.
- **Mandatory Methodology Note**:
  *Connections are inferred from neighboring messages and do not prove direct replies or real-world relationship strength.*

---

## 6. Vocabulary & Recurring Phrase Candidates

### Tokenization & Stopwords
- **Tokenization**: Unicode-aware letter sequence extraction (`\p{L}+`). Strips URLs, email addresses, and punctuation.
- **Stopwords**: Curated lists of high-frequency English and Arabic functional words (pronouns, prepositions, common conjunctions).
- **N-Grams**: Contiguous sequences of 2 words (bigrams) or 3 words (trigrams) from the same message.

### Recurring Phrase Candidates ("Inside Jokes")
- **Definition**: Multi-word phrases repeated across multiple conversation sessions.
- **Type**: Exploratory Lexical Candidate.
- **Candidate Ranking Criteria**:
  1. Phrase frequency $\ge 3$ occurrences.
  2. Multi-member usage: used by $\ge 2$ distinct participants.
  3. Span: used across distinct dates.
- **Limitations**: Surfaced purely through statistical repetition. May include common idiomatic expressions, greeting formulas, or meeting logistics in addition to genuine inside jokes.
