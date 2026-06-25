# BIVREST Data Annotation Guide for AI

**Method Author:** Olesya Lazareva  
**Version:** 1.0

---

## 1. What This Is

BIVREST generates a unique type of data: each participant action receives a binary **"Believe / Don't Believe"** label from the group (or from an AI verifier).

This provides **ground truth** for training:

- congruence detectors (role-behavior alignment)
- emotion recognition models
- behavioral analytics systems
- AI verifiers of role consistency
- persuasiveness classifiers

---

## 2. Data Format

A single session log includes the following fields (unified with the protocol specification):

| Field | Type | Description |
|---|---|---|
| `session_id` | string | Unique session identifier |
| `timestamp` | datetime | Date and time of the move (ISO 8601) |
| `round` | integer | Round number |
| `player_id` | string | Anonymous player ID |
| `avatar` | string | The role the participant is playing |
| `task` | string | Task text |
| `action_text` | text | Player action (verbal or description of physical action) |
| `votes_believe` | integer | Number of "Believe" votes |
| `votes_dont_believe` | integer | Number of "Don't Believe" votes |
| `verdict` | string | Result: "Believe" or "Don't Believe" |
| `tokens_lost` | integer | Number of tokens lost (penalty) |
| `empty_chair` | boolean | Whether "Empty Chair" was activated (true/false) |
| `notes` | text | Additional notes (optional) |

### CSV Example (Header + Data)

```csv
session_id,timestamp,round,player_id,avatar,task,action_text,votes_believe,votes_dont_believe,verdict,tokens_lost,empty_chair,notes
S001,2026-06-25T12:00:00,1,P001,Little Red Riding Hood,Reveal avatar's secrets,"She's shy, whispering her fantasies to the trees",3,1,Believe,0,false,
S001,2026-06-25T12:05:00,2,P002,Elite Escort,Make a provocative offer,"You look expensive. Very expensive.",4,0,Believe,0,false,
S001,2026-06-25T12:10:00,3,P001,Little Red Riding Hood,Seduce the wolf,"Dear wolf, what a long... nose you have",1,4,Don't Believe,1,false,Group considered it out of character
S001,2026-06-25T12:20:00,4,P003,Wolf,React to provocation,"I can't be held responsible for myself...",2,3,Don't Believe,2,true,Role exit
3. Collection Recommendations
Anonymization
Replace participants' real names with P001, P002, P003

Do not store any identifying information

Completeness
Record all moves, including "failed" ones (sabotage, refusal, laughter)

Even if a player drops out of role — record it

Timestamps
Record the time of each move for dynamic analysis

Context
Briefly describe non-verbal actions in the notes field or in action_text in square brackets

Example:

text
[Laughing, blushing, turning away] "Well, I don't know..."
4. Use Cases for AI Training
Task 1. Congruence Classification ("Believe / Don't Believe")
Train a model to predict the group verdict based on action_text and avatar.

text
Input: avatar, task, action
Output: "Believe" / "Don't Believe"
Example Data:

csv
text,role,task,label
"She's shy, whispering her fantasies to the trees","Little Red Riding Hood","Reveal avatar's secrets","believe"
"Dear wolf, what a long... nose you have","Little Red Riding Hood","Seduce the wolf","dont_believe"
Task 2. Sabotage and Role Exit Detection
Train a model to recognize:

Type	Indicators
Pretending	Player avoids engagement, doesn't commit to role
Evasion	Overly generic phrases, jokes, topic shifting
Role mismatch	Action doesn't match expectations for the role
These cases are often accompanied by:

verdict = "Don't Believe"

tokens_lost > 0

empty_chair = true

Task 3. Emotion Recognition (Extended Annotation)
For this task, annotate actions on additional scales:

Scale	Range	Description
Shame	0–10	How much shame/embarrassment is present
Fear	0–10	How much fear/anxiety is present
Arousal	0–10	How much sexual or emotional arousal is present
Engagement	0–10	How immersed the player is in the role
Example Annotation:

csv
action_text,avatar,task,label,shame,fear,arousal,engagement
"She's shy, whispering her fantasies to the trees","Little Red Riding Hood","Reveal secrets","believe",6,2,1,8
"You look expensive. Very expensive.","Elite Escort","Make a compliment","believe",1,1,7,9
5. Dataset Formats
5.1. CSV (Basic)
csv
text,role,task,label,session_id,round
"She's shy, whispering her fantasies to the trees","Little Red Riding Hood","Reveal avatar's secrets","believe","S001",1
5.2. JSONL (for LLMs)
jsonl
{"text": "She's shy, whispering her fantasies to the trees", "role": "Little Red Riding Hood", "task": "Reveal avatar's secrets", "label": "believe", "session_id": "S001", "round": 1}
5.3. Extended JSONL (with emotion scales)
jsonl
{"text": "She's shy, whispering her fantasies to the trees", "role": "Little Red Riding Hood", "task": "Reveal avatar's secrets", "label": "believe", "shame": 6, "fear": 2, "arousal": 1, "engagement": 8}
6. Annotation Quality Control
Recommendations
Method	Description
Double annotation	Two independent annotators label the same data
Agreement calculation	Cohen's Kappa > 0.8 indicates good agreement
Expert review	A third expert reviews ambiguous cases
Annotator Checklist
Before saving a record, check:

action_text contains the complete roleplay

avatar matches the role from the log

task matches the assigned task

label matches the verdict (believe / dont_believe)

tokens_lost is a number, not "yes/no"

empty_chair is true or false, not "yes/no"

7. Ethical Requirements
Informed Consent

Data is collected only with participant consent

Participants may delete their logs at any time

Confidentiality

Data is not shared with third parties without consent

All data is anonymized

Prohibited Uses

It is strictly forbidden to use the data for:

creating systems to assess "sexual deviance"

discriminatory purposes

publicly revealing participant identity

8. Commercial Use
For training your models on data generated by BIVREST, agreement with the method author is required.

Contacts: Olesya Lazareva

Telegram: @olesyalazarevalove

Email: psi-tech@yandex.com

9. Versioning
