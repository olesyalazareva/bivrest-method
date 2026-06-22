# BIVREST API Reference

## Overview

This API enables digital implementation of the BIVREST method for Telegram bots, web applications, and automated data collection systems.

**Important:** Commercial use of this API requires permission from the method author.

---

## Authentication

For non-commercial research and open-source projects, no authentication is required. For commercial implementations, contact the author for API keys.

---

## Endpoints

### POST /session/start

Initiates a new game session.

**Request:**
```json
{
  "players": [
    {"id": "P001", "avatar": "Little Red Riding Hood"},
    {"id": "P002", "avatar": "Mistress"}
  ],
  "stakes": 6
}
Parameters:

Field	Type	Description
players	array	List of players with their avatars
stakes	integer	Initial number of "Chances" per player
Response:

json
{
  "session_id": "S001",
  "turn_order": ["P001", "P002"]
}
Field	Type	Description
session_id	string	Unique session identifier
turn_order	array	Turn order for the session
POST /turn/act
Executes a player's turn.

Request:

json
{
  "session_id": "S001",
  "player_id": "P001",
  "card": "Two of Clubs",
  "action": "She's shy, whispering her fantasies to the trees..."
}
Parameters:

Field	Type	Description
session_id	string	Session ID
player_id	string	Player ID
card	string	Card name (as in the game)
action	string	Text description of the action
Response:

json
{
  "verdict": "Believe",
  "votes": {"Believe": 3, "Don't Believe": 0},
  "penalty": 0,
  "empty_chair": false
}
Field	Type	Description
verdict	string	Voting result: "Believe" or "Don't Believe"
votes	object	Vote distribution
penalty	integer	Penalty in "Chances"
empty_chair	boolean	Is "empty chair" mode activated
POST /turn/verification
Requests AI evaluation of action authenticity.

Request:

json
{
  "avatar": "Little Red Riding Hood",
  "task": "Describe your avatar's sexual life",
  "action": "She's shy, whispering her fantasies to the trees...",
  "previous_failures": 0
}
Parameters:

Field	Type	Description
avatar	string	Role the player is acting as
task	string	Task from the card
action	string	Player's action
previous_failures	integer	Number of previous "Don't Believe" votes in this session
Response:

json
{
  "verdict": "Believe",
  "confidence": 0.87,
  "reason": "Action contains sensory markers (pine scent) and emotional coloring, consistent with Little Red Riding Hood character"
}
Field	Type	Description
verdict	string	"Believe" or "Don't Believe"
confidence	float	AI confidence (0.0–1.0)
reason	string	Verdict justification
POST /session/empty_chair
Activates "empty chair" mode (after two consecutive "Don't Believe" votes).

Request:

json
{
  "session_id": "S001",
  "player_id": "P003",
  "stimulus": "What are you really afraid of?"
}
Parameters:

Field	Type	Description
session_id	string	Session ID
player_id	string	Player ID
stimulus	string	Question or task from the facilitator
Response:

json
{
  "response": "I'm afraid that if I ask, they'll reject me. I've always been shy to ask.",
  "new_script": "I can ask if I want to"
}
Field	Type	Description
response	string	Player's first-person response
new_script	string	Recorded new behavioral script
GET /session/log
Retrieves complete session log for AI training.

Request:

text
GET /session/log?session_id=S001&format=csv
Parameters:

Parameter	Type	Description
session_id	string	Session ID
format	string	json or csv (default: json)
Response (CSV):

csv
session_id,timestamp,player_id,avatar,task,action,votes_trust,votes_not_trust,verdict,penalty,empty_chair,new_script
S001,2026-04-01T12:00:00,P001,Little Red Riding Hood,Describe avatar's sexual life,"whispering to trees...",3,1,Believe,0,0,
S001,2026-04-01T12:05:00,P002,Mistress,Make a compliment,"You look expensive",4,0,Believe,0,0,
Error Codes
Code	Description
400	Invalid request format
401	Unauthorized access (for commercial implementations)
404	Session or player not found
429	Too many requests
Rate Limits
Non-commercial: 100 requests per minute

Commercial: Contact the author for custom limits

License & Terms
Non-commercial use (research, open-source) — Free with attribution.

Commercial use (selling digital products based on BIVREST) — Requires agreement with the author.

For commercial licensing: @olesyalazarevalove (Telegram)

Related Documentation
Full protocol: /protocol/BIVREST_method.md

Game rules: /game/Universe69_rules.md

Annotation guide: /annotation-guide/README.md

Related project: UNIVERSE 69
