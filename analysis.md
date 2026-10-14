# Analysis

---

## Problem identification
Wordbomb, a multiplayer word game where a pattern of 2 random letters are presented. A player should try and enter a valid word containing the 2 random letters within an increasingly small time limit. Failiure to do this means the 'bomb' goes off and that player loses the game. Players should take it in turns, with new patterns each round until the last player standing is crowned winner.

Groups of school students want a quick competetive game against eachother, school computers dont allow personal downloads thus it must be a web game. Existing web games include

- Research A
Netlify Word bomb [https://wordbomb.netlify.app/]
| Strengths | Weaknesses |
| --- | --- |
| Readable, easy to navigate UI. | The buttons have no use, purely cosmetic |
| Ample cusomisation, can choose from avatars | Doesn't indicate room code format, not accessible for new players |
| Limited username size, no long usernamed people ruining game | |

- Research B
JKLM Word bomb [https://jklm.fun/]
| Strengths | Weakness |
| --- | -- |
| Easy party UI navigation | Censored chatting, spamming in chat |
| Animations improve user experience | Custom pfp's include NSFW content |
| Leaderboard system improves competitivy | No private rooms, stuck with random players |

- Research C
Wordbomb.io [https://wordbomb.io/]
| Strengths | Weakness |
| --- | --- |
| Customisable animations | Uncensored chatting, slurs lower user experience |
| Reward system, improves replayability | Paid currency, in app purchases |
| Previous word history, removes annoying aspect of game | Frequent cheaters |

- Research D
Roblox Word bomb [https://wordbomb.io/]
| Strengths | Weakness |
| --- | --- |
| Well polished UI | Heavily censored chatting, uncommunicatable |
| Easy multiplayer joining | No customisation | 
| | Cheaters |

---

## Computational approach
A computational approach can be deemed suitable for Wordbomb

| Technique | What it is | Application  
| --- | --- | --- |
| Abstraction | Removing unnecessary details | Simplified to just players, lives, current pattern, used words and timer |
| Thinking ahead | Finding inputs and outputs | Handling input word, join code, valid/invalid words and scores | 
| Procedural thinking | Breaking problems into subproblems | Accounts, lobby, game loop, validation, prompt generation, rendering, persistence |
| Logical thinking | Decisions and conditions | Word valid if in dictionary AND contains prompt AND unused |
| Concurrency | Tasks running at the same time | Many parties at once, timers running while players type, websocket events arriving simultaneously | 



> Abstraction - diagram of abstract game model
> Thinking ahead - input output table
> Prodedural thinking - decomposition tree
> Logical thinking - truth table / flow chart
> Concurrency - Sequence diagram of two parties

---

## Stakeholders
I conducted an interview in person with my target audience, placing emphasis on variety to get a broad scope of requirements

- Stakeholder 1 / S1
| Field | Entry |
| --- | --- |
| Name | Joel Hampstead | 
| Age | 17 |
| Experience | Frequent multiplayer game enjoyer |	
| Device | Computer |
| Use case | Weekly lunchtime games with friends | 
| Suitability | Accessible and no learning curve |

- Stakeholder 2 / S2
| Field | Entry |
| --- | --- |
| Name | James Tobin | 
| Age | 15 |
| Experience | Roblox Wordbomb enthusiast |	
| Device | Computer, phone, tablet |
| Use case | Daily playing during/afterschool | 
| Suitability | Playable on any device and portable (as long as wifi) |

- Stakeholder 3 / S3
| Field | Entry |
| --- | --- |
| Name | Julian Szmulka | 
| Age | 17 |
| Experience | Hosts games night's with friends |	
| Device | Phone |
| Use case | Organizing and hosting matches | 
| Suitability | Easy party creation and management |

> Justify how affected requirements

--- 

## Research methods
To test how much word bomb appealed to my target audience, I conducted a tallied survey asking students which games they play during school.
| Game | Tally |
| --- | --- |
| Knock off Fortnite | 9 |
| Knock off Minecraft | 9 |
| Run | 9 |
| Cps/WPM tests | 4 |
| Knock off GTA | 2 |
| Papas Pizzaria | 7
| Gswitch | 8 |
| Wordle/NYT Games | 9 |

The most popular games were almost all multiplayer (Fortnite, Minecraft, Gswitch) or word/skill games (Wordle/NYT games, Cps/WPM tests) thus Wordbomb (which lies between both) is suitable for this audience

Next I conducted a questionnaire
| Question | Purpose |
| --- | --- |
| How old are you | Compares realism of responses |
| How would you like to access the video game | Decides platform |
| How much time per round | Default round time | 
| How many players per game | Sets player cap |
| How many letters per pattern | Default round letters |
| Do you want to play against bots | Prioritise features |
| Do you want a leaderboard | Prioritise features |

> Justify how affected requirements

Finally I observed my stakeholders play existing games.
| Observation | Implication |
| --- | --- |


---

## Existing solutions research
To gain a broad spec of necessary features, I compared 2 of the 4 existing solutions
| Aspect | JKLM | Wordbomb.io | Takeaway |
| --- | --- | --- | --- |
| Accounts | Username, no login | Login, persistant currency | Login too complex, just username will do |
| Party size | 16 | 32 | Limit of 16 to preserve bandwidth |
| Rules | Language, pattern copmlexity, turn duration, Life count | Custom language, no other rule customisation | Language, pattern complexity, turn duration and life count necessary |
| Mobile support | Fits phone screen, phone keyboard support | Fits phone screen, phone keyboard support | Use phones in built keyboard if implementing mobile |
| Ads/cost | No ads, no in-app purchases | No ads, premium currency for cosmetics | No ads or purchasables necessary | 
| Visual feedback | Visual timer in middle of screen, pattern displayed at top | Visual timer in middle of screen, animations, pattern displayed at top | Must follow a similar layout |
| Reconnection handling | Prompts reload which returns to game, no immunity | Prompts reload which leads to spectating | Game state should be persistant regardless of reloads |

---

## Essential features
| ID | Feature | Priority | Justification |
| --- | --- | --- | --- |
| F1 | Username | Essential | Solutions research | 
| F2 | Create party with a short join code | Essential | S3 needs easy hosting | 
| F3 | Join party via code, with nickname | Essential | S2 wants quick join times | 
| F4 | Real-time game: prompt, word entry, timer, lives | Essential | Core game aspect | 
| F5 | Server-side word validation (dictionary, contains prompt, not reused) | Essential | Fairness, Research C & D | 
| F6 | Animated canvas: player circle, bomb, fuse, explosion | Essential | Observation: visual feedback valued | 
| F8 | Persistent game history and results | Desired  | S2 | 
| F10 | Reconnection and host migration | Desired | Solutions research | 
| F11 | Bonus letters / extra lives | Optional | Research B | 
| F12 | Sound effects and mute option | Optional | S1 needs Accessibility | 
| F13 | Mobile-friendly controls | Optional | S1 needs Accessiblity | 
| F14 | Spectator mode, custom dictionaries | Won't | Out of scope |

---

## Limitations
| Limitation | Reason | Impact |
| --- | --- | --- |
| English dictionary only | Licensing and scope | Non-English users excluded |
| 8 Player cap | Cutting bandwidth and hardware | Larger groups cannot play together |
| No mobile layout| Time constraints | Phone users need a desktop browser |
| No voice or text chat | Out of scope, moderation risk | Players use external chat | 
| Single server host | Hosting budget | Party number capped |
| Cheating via external word lists cannot be fully prevented | Server cannot detect outside help | Only timing/validation fairness is enforced |

---

## Requirements
- Hardware/software
| Category | Requirement | Justification | 
| --- | --- | --- | 
| Server | Machine capable of running Node.js and MySQL | Handles many concurrent parties |
| Server software | Node.js LTS, MySQL 8, npm packages | Stated stack | 
| Client hardware | Any device with a modern browser; keyboard for typing | Word entry | 
| Client software | Browser supporting HTML5 Canvas and WebSockets | Rendering and communication | 
| Network | Stable internet; target round-trip latency under 150 ms | Real-time fairness | 
| Development tools | Nvim, Git/GitHub, MySQL Workbench | Evidence of process | 

- Stakeholder requirements
| ID | Requirement | Source | Linked feature |
| --- | --- | --- | 
| R1 | Players can join a party using a code of 4-6 characters | S1, Q8 | F2, F3 | 
| R2 | A party supports 2 to 8 players | Q3 | F4 |
| R3 | Turn time is configurable between 5 and 30 seconds | Q5 | F7 |
| R4 | Invalid words give clear feedback stating the reason | Observation | F5, F6 |
| R5 | Game results persist during reloads | S2 | F8 |










