---
name: sw-workflow
description: Project orchestrator for the screenwriting skill set — a meta-skill that adds no new craft knowledge but routes a screenplay or stage-play project through stages (premise, structure, character, scenes, draft, revision, submission) and a TV or streaming series project through a separate series stage table (engine, character network and season arc, documents/bible, pilot structure, break story and outline, draft, submission), names which sw-* skill to invoke at each stage, defines each stage's deliverable and advisory exit check, and keeps all project state in a story-bible.md file so work can resume across sessions. Use when starting a new script project, resuming one, when the user asks 'what should I do next' on a script, when converting a vague idea into a full development pipeline, or when the other sw-* skills are firing individually and the overall process needs sequencing.
---

# Workflow & Story Bible

This skill contains no new screenwriting knowledge. It does two things only: **put the work in order** (which skill to call at each stage, what to deliver, what counts as passing) and **store state** (write each stage's conclusions into `story-bible.md` so the next session can continue). All methods live in the other sw-* skills; this skill is responsible only for calling them at the right moment.

The design is based on a controlled experiment: for the same assignment, a process that fills in worksheets before writing, compared with writing directly without a process, produced different results in length, protagonist agency, opponent strength, and subtext. The difference is not knowledge; it is "the forms that must be filled in before writing and the checklist that must be passed after writing." This skill is the dispatcher for that form and that checklist.

The story-bible template and the worksheets for each stage are in [reference.md](reference.md); the terminology anchor table for cross-language output is in [terms.md](terms.md).

---

## 1. Session Protocol (run at every start and end)

### Start

1. Look for `story-bible.md` in the current directory (or the script directory the user specifies).
2. **If found:** read only the three sections "Current Stage," "Decided Decisions," and "Decision Log," and summarize the project to the user in three sentences: what the project is, how far it has gone, and what was decided last time. Then go directly to the current stage. Do not reopen decided decisions unless the user explicitly overturns them.
3. **One-off delivery does not need a bible:** the user wants a document delivered on the spot (a development plan, a proposal, a one-page synopsis, an episode outline), and there clearly will be no next session to continue it. In that case building a bible is a net cost; just run the stage table in the same session. The bible solves **loss of context across sessions**, not "the process must have a form."
4. **If not found and this is an ongoing project:** determine the entry path (see Section 3), create `story-bible.md` from the template in reference.md, and fill in only "Project Information" and "Current Stage"; leave the rest blank. Do not ask the user more than four questions at once; infer what you can from what the user has said, fill it in, and mark it "(to be confirmed)."

### In Progress

- Whenever a stage deliverable is completed, write it immediately into the corresponding section of the story-bible and advance "Current Stage" by one step.
- Any action that changes an established decision (changing the premise, changing the ending, deleting a character) gets a new line in the "Decision Log": date, what changed, why.
- Keep the story-bible short enough to read in one sitting (about 25K tokens; under 15,000 Chinese characters). Record conclusions only, not the reasoning process. Outlines, treatments, and script pages go in separate files; the bible records only the file name and a one-line status.

### End

- Before the session ends, confirm that the story-bible is up to date, and write a final line: "Next step:" followed by one sentence.

---

## 2. Stage Map

| # | Stage | Skill invoked | Deliverable (section written into the story-bible) | Suggested passing standard |
|---|---|---|---|---|
| 0 | Start / resume | This skill | Project information, entry path, current stage | Know the genre, length, and audience |
| 1 | Material and premise | `sw-premise-theme` | Spark and "why I care," one-sentence theme, hypothetical question, **premise** (character trait + cause + outcome), **controlling idea** (value + cause), third rail (desire vs. misbelief), xìhé (the core premise), one-sentence story, logline | Only one premise; can be explained to a stranger in one sentence; removing the xìhé makes the play collapse; the theme words are fixed |
| 2 | Structure | `sw-story-structure` | Ending, opening, plot points I/II, nature of the midpoint (false victory / false defeat), BS2 page table, act proportions, relationship of subplot to controlling idea | Know all four things (ending / opening / two plot points); setup ≤ 25 pages; midpoint and "all is lost" are opposites; the last act is the shortest |
| 3 | Character and conflict | `sw-character-conflict` | Three-dimensional table for major characters, specific categories, attitude toward the theme, unity-of-opposites binding object, the opponent's knife, growth ladder, original scene | The protagonist has the most dimensions; the opponent's sum is stronger than the protagonist; no two characters are the same type; there is a "the strongest opponent is oneself" side; no xiángyún (deus ex machina) |
| 4 | Scene list / treatment | `sw-scene-craft` + `sw-format-adaptation` | Step outline (one or two sentences per scene + value turn + structural position), 40-card board (+/−, ><), props and image system, treatment (optional) | Every scene has a value turn; the third act has more than two cards; adjacent scenes have transitional elements; no scene that is pure exposition |
| 5 | First draft | `sw-dialogue` + `sw-format-adaptation` (format and output contract) + reference skills | Script file (Hollywood style delivered as `.fountain`; Chinese numbered-scene format or Japanese format delivered as plain text; see `sw-format-adaptation` Section 2.2), page count, daily progress | Page count within ±15% of target; all hard format rules pass; dialogue is distinguishable with names covered |
| 6 | Revision | The "diagnostic checklist" in each skill | Revision target list, item-by-item completion record, draft number | Structure diagnostic 13 questions, character diagnostic 14 questions, dialogue diagnostic 14 questions, scene diagnostic 13 questions, format diagnostic (A: 12 general questions + the group for the chosen format) all run once |
| 7 | Submission / industry | `sw-industry-business` | Logline and one-page synopsis, pitch document, target buyers/competitions, credit and registration | PROBLEM seven-element self-check passes; the one-sentence story passes the stranger test |

**When reference skills enter:**
- `sw-american-case-studies`: Stages 1–2, to find comparable films and clichés in the same genre; Stage 6, to compare climaxes in the same genre.
- `chekhov-dramaturgy`, `ozu-screenplay-style`: when writing anti-climax, multiple protagonists, family material, or "events off-screen, reactions on-screen," use them as models for structure and tone from Stage 2.
- The four Chinese-opera skills (`sw-chinese-opera-banqiang`, `sw-chinese-opera-qupai`, and the two `-cases` skills): when the project is Chinese opera, do not use the feature-film stage table in this section; use the X table or Q table in Section 3.3. The medium-boundary table at the start of the two method skills determines which layers of the general skills can be used.
- `sw-japanese-screenwriting`, `sw-korean-french-screenwriting`: alternative paths such as fragment-first, theme-later, genre promise, and collective creation; introduce them at Stage 1 when the user explicitly does not want the classic three-act design.
- `sw-truby-anatomy` (organic story anatomy): run the page map and the organic skeleton side by side — after the BS2 board is finalized in Stage 2, do the organic check (the seven key steps in reverse + the mid-story components of the 22 steps); in Stage 3, pair the character table with the four-corner opposition worksheet; in Stage 4, the structural-position column of the step outline can carry the 22-step names + line numbers; in Stage 6, run its ten diagnostic questions if the middle sags. Chekhov/Ozu-style anti-climax, multiple-protagonist projects, and series projects do not use its central-battle component.
- `sw-genre-anatomy` (genre anatomy): Stage 0, set the primary and secondary genres; Stage 1, compare the controlling idea with that genre's life philosophy; Stage 2, after the structure is finalized, run that genre's beat sheet and the genre-mixing worksheet; Stage 3, compare the character table with that genre's protagonist/opponent template; Stage 6, run the 12 genre diagnostic questions. For series, take only the four series conclusions it identifies; Chinese opera and anti-climax projects do not use the beat sheet.
- Series skills (`sw-series-structure`, `sw-series-engine-bible`, `sw-writers-room`, `sw-sitcom-comedy`, `sw-chinese-series-practice`, `succession-series-writing`, `sw-series-case-studies`): enter only when the entry path is judged to be a series; use the series stage table in Section 3.2.

**Stages can move backward:** if dialogue will not come in Stage 5, the problem is usually a hole in the Stage 3 characters or the Stage 1 premise. Go back and fix it, then record a line in the decision log.

---

## 3. Entry Paths

| User situation | Stage to start from | Special handling |
|---|---|---|
| Writing a feature / multi-act play from scratch | 0 → 1 → … → 7, all stages | Standard path |
| Already has a first draft to revise | First do **reverse filling** of Stages 1–3 (extract premise, structure, and characters from the draft into the bible), then go to Stage 6 | Mark missing items as "missing" while filling; those missing items become the revision list |
| Adapting a novel / stage play / true event | 0 → `sw-format-adaptation` four adaptation questions → 1 → 2 … | At Stage 1, first answer "at what level does the source material's conflict mainly sit, and what must be reinvented"; for a true story, confirm rights first; **Chinese-opera material does not use this row; use X0.5/Q0.5 in Section 3.3** |
| Short film / short play / one-act play | 1 → 2 (use Lu Jun's qǐ chéng zhuǎn hé and eight methods instead of BS2) → 3 → 5 | Shrink the board to 10–15 cards; ≤ 5 characters; the xìhé must exist first |
| Chinese opera · banqiang system (Peking opera / Henan opera / Yue opera / Qinqiang / Pingju / Shanghai opera / Sichuan opera's huqin style) | Use **banqiang X0–X6** in Section 3.3, not the feature-film stage table | Fix the system before the structure; arias only for heavy scenes; spoken dialogue uses `sw-dialogue`, lyrics and metrical patterns use `sw-chinese-opera-banqiang`; for full-script comparison see `sw-chinese-opera-banqiang-cases` |
| Chinese opera · qupai system (Yuan zaju / Ming–Qing chuanqi / Kunqu / Sichuan opera high-pitched style) | Use **qupai Q0–Q6** in Section 3.3 | First answer two switches: "stage or page" and "zaju or chuanqi"; tune-filling uses `sw-chinese-opera-qupai`; for full-script comparison see `sw-chinese-opera-qupai-cases`; for Sichuan opera scripts, consult both tables |
| Only an idea, unsure whether it can be written | 1 (only up to the one-sentence story) → the PROBLEM self-check in 7 | If it passes, return to 2; if it fails, change the idea and keep the rejected idea and the reason in the bible |
| TV drama / series / pilot / one season | Use the **series stage table** (S0–S7) in Section 3.2, not the feature-film table above | Engine and bible come before the script; mainland Chinese series add the document chain in `sw-chinese-series-practice`; for the proposal format, see the Omiya Ellie template in the `sw-format-adaptation` reference |
| Half-hour comedy / sitcom | Series stage table, but replace S2 and S5 with `sw-sitcom-comedy` | Page count, format, and joke density all switch |
| Industry question (how to sell, credit, agent) | Go directly to 7 | Do not build a bible |

### 3.2 Series Stage Table (TV drama / streaming series / miniseries)

The difference between a series and a feature is not "a longer movie": a film is a closed arc and a one-time problem; a series is a repeatable **engine** plus open-ended relational tension, cut into segments by act outs, with multiple storylines running in parallel, the bible before the script, and collective creation coordinated by the showrunner. So the order is reversed: **first prove that the engine can run for a hundred episodes, then write the first episode.**

| # | Stage | Skill invoked | Deliverable (section written into the story-bible) | Suggested passing standard |
|---|---|---|---|---|
| S0 | Start / resume | This skill | Platform and format (broadcast / cable / streaming; one-hour / half-hour; episode count, season count), entry path | Know who determines the act count (advertising slots or the writers) and the target page count |
| S1 | Engine and premise | `sw-series-engine-bible` + `sw-premise-theme` | Thematic counter-proposition, franchise four elements (concept / conflict / theme / story pattern), core question written as a "process sentence," one-sentence tacit contract, 5–6 sample story areas | "Cannot think of three episodes after the pilot" = fail; if the five story areas have the same source or the same ending = fail |
| S2 | Character network and season arc | `sw-series-engine-bible` + `sw-character-conflict` | 3–4 protagonists (≤ 1 page each) and the conflict network (who is bound to whom, specialty division, family dynamics), season arc table (episode × character want/state), season question and tentpole | Protagonists cannot "smile and agree with each other"; each has something to lose; the season ending answers "the question of this year's version," not the overall question |
| S3 | Documents | `sw-series-engine-bible` (+ `sw-chinese-series-practice` for mainland Chinese series) | Logline and springboard, pitch document / series format, bible (chosen tier), story-line document (purpose / driver / entry and exit / cross-episode beats for each line); mainland Chinese series also deliver synopsis → outline → character biographies → episode outline | The documents let a stranger retell "what will happen each week"; each episode of a mainland Chinese series outline has a closing hook |
| S4 | Pilot and episode structure | `sw-series-structure` (replace with `sw-sitcom-comedy` for half-hour comedy) | Pilot type choice (premise / typical-episode / hybrid), act count and page anchors, act-out list, entry and exit of A/B/C stories, Story Map 17 columns | Every act out raises a new question; the C story does not close an act; the invisible act can state three grounds |
| S5 | Break story and outline | `sw-writers-room` + `sw-scene-craft` | Beat sheet (6–7 scenes per act) → outline (locked); six-week schedule per episode | Each outline scene has one beat and its position within the act; changing the ending requires returning to the outline |
| S6 | First draft and revision | `sw-dialogue` + `sw-format-adaptation` + `sw-writers-room` (handling notes) | Script file (teaser / ACT markers or day markers), page count, warm-read and cold-read records | Page count within the format range (one-hour 48–63; half-hour single-camera ≈ 30; multi-camera ≈ 50); a cold read can answer "what is the next episode?" |
| S7 | Submission / industry | `sw-industry-business` (US) / `sw-chinese-series-practice` (mainland China: project registration, filing, censorship, delivery milestones) | 20-minute pitch script, one-page leave-behind, target platform list | Pitch only one project per meeting; self-check against both content and technical censorship for mainland Chinese series |

**When reference skills enter:** `succession-series-writing` (streaming ensemble, invisible acts, season-shape symmetry, ending engineering) serves as a model from S2; `sw-series-case-studies` (The West Wing's four acts, the Sopranos pilot, Downton's multiple storylines, Fleabag's six-episode season, Calvisi's eight pilot beat sheets, Sakamoto Yuji, Noh Hee-kyung) is used to find comparable shows at S1 and to compare beats at S4. `chekhov-dramaturgy` and `ozu-screenplay-style` are **cross-stage general references** (not exclusive to features): when writing anti-climax, multiple protagonists, family material, or "events off-screen, reactions on-screen," the series track also calls them from S2, but first pass the capacity prerequisites and series conversion in `ozu-screenplay-style` Sections 2.1 and 2.14. **The medium-independent parts of the feature skills still apply**: dialogue, scene value turns, three-dimensional characters, premise — do not skip them just because the project is a series.

**Division of the two scene-level tool sets at S5:** for scene-level work in series, **prefer the five-piece set in `sw-series-structure` Section 6** (one purpose per scene, entry and exit points, value turn, information gap, hook to the next scene), and run it scene by scene when breaking the beat sheet and writing the outline; add the **40-card board and "what happens if I delete it" from `sw-scene-craft` after the outline takes shape** (the 40 cards are spread across the season's episode count, not 40 cards per episode) to delete scenes without value turns. Skipping both counts as a missed step; running only the five-piece set does not count as complete.

**Backtracking:** if S4 cannot produce act outs for a second episode, it is usually an S1 engine problem; if dialogue will not come in S6, it is usually because the S2 character network has nothing to lose. Go back and fix it, and record it in the decision log.

### 3.3 Chinese Opera Stage Table (banqiang / qupai)

Chinese opera does not use the feature-film stage table or the series stage table: its structural unit is the 场 (chǎng — scene), 折 (zhé — act), or 出 (chū — scene); arias come before dialogue; the system (song-heavy play or action-heavy play) comes before structure; and **you must determine the vocal system before choosing a skill**. How to decide: Peking opera, Henan opera, Yue opera, Qinqiang, Pingju, Shanghai opera, and Sichuan opera's huqin style → banqiang system (X table); Yuan zaju, Ming–Qing chuanqi, Kunqu, and Sichuan opera's high-pitched style → qupai system (Q table); a single Sichuan opera script may cross both systems, so consult both tables. The methods for both tables are in `sw-chinese-opera-banqiang` and `sw-chinese-opera-qupai`; the full-script corpora are in `sw-chinese-opera-banqiang-cases` and `sw-chinese-opera-qupai-cases`; the aesthetics and rehearsal layer shared by both systems are in `sw-chinese-opera-banqiang/reference-common.md`.

**Banqiang X0–X6**

| # | Stage | Skill invoked | Deliverable (section written into the story-bible) | Suggested passing standard |
|---|---|---|---|---|
| X0 | Start | This skill | Opera genre, system, whether it is a new work / restoration of an old play / modern play / commissioned adaptation, and for which performer or role type it is written | The genre and system are unambiguous; the script format is set as Peking-opera style or Yue-opera style |
| X0.5 | Real-person / historical material (do if applicable) | `sw-chinese-opera-banqiang` (Section 11, four adaptation questions) | A comparison table: whether each plot point is historical record, legend, or invented; the largest fictional invention and its constraints | Fiction occurs only in the gaps of the historical record; do not excuse the protagonist; the four questions are answered inside the opera skill, not in `sw-format-adaptation` |
| X1 | Set the system | `sw-chinese-opera-banqiang` (system and genre) + `sw-premise-theme` (xìhé) | One of song-heavy / action-heavy / martial / balanced, with grounds (character action and role type, plot complexity and dance conditions, style); one-sentence xìhé | Fix the system before moving on; the "develop in the same direction" self-check passes (do not go against the genre's temperament) |
| X2 | Main line and technical structure | `sw-chinese-opera-banqiang` (concentration of the main line, technical structure and staging) | One-sentence main line (vertical concentration); scene table (event per scene + proportions of song/speech/action/martial + hot/cold); two or three heavy scenes; list of transitions | The staging-alternation law passes; metrical sections are concentrated in heavy scenes; transitions do not add arias for the protagonist |
| X3 | Role types and characters | `sw-chinese-opera-banqiang` (role type determines writing, writing for the performer) + `sw-character-conflict` | Character table with role types; the lead performer's skill list and repertoire gaps; role-type taboo check | No violation of taboos such as a 净 (jìng — painted-face) role singing 反二黄 (fǎn'èrhuáng); one-actor-multiple-roles (if any) is viable |
| X4 | Aria design | `sw-chinese-opera-banqiang` (lyrics, duets, what the playwright must mark) | Aria table (scene / character / intended metrical pattern / line count / rhyme category); write each passage's key line first; placement of 垛句 (duǒjù — inserted short lines); rhyme-category layout for the whole play | The paired-line phrasing passes; the second line rhymes, the first may not; odd-numbered lines only at 扫头 (sǎotóu); duet passages have a diminishing or confrontational structure |
| X5 | First draft | `sw-chinese-opera-banqiang` (speech-to-song seam, use of conventions) + `sw-dialogue` (spoken dialogue) + `sw-chinese-opera-banqiang-cases` (comparison corpus) | Script (song / speech / stage cues; if Peking-opera style is chosen, also mark metrical patterns and gong-drum patterns; for Yue-opera style or no metrical marking, see `sw-chinese-opera-banqiang` Section 9) | The line before each aria is an address term; the convention-selection list is explicit; modern plays omit self-introduction and entrance poems |
| X6 | Tune review and revision | `sw-chinese-opera-banqiang` (interface with performers and musicians, diagnostic checklist) | Revision record; note that metrical markings are letters of intent, and changing words requires changing the tune | The diagnostic checklist is complete; where opinions differ, note which side was chosen |

**Qupai Q0–Q6**

| # | Stage | Skill invoked | Deliverable | Suggested passing standard |
|---|---|---|---|---|
| Q0 | Start | This skill | Zaju, chuanqi, or a Kunqu excerpt; stage or page (dramatic qu vs. pure song); newly filled or adapted from an old script | Both switches answered |
| Q0.5 | Real-person / historical material (do if applicable) | `sw-chinese-opera-qupai` (adaptation and rewriting) + `sw-chinese-opera-banqiang` Section 11, four adaptation questions | Same as X0.5: historical record / legend / invention comparison table | Same as X0.5 |
| Q1 | Establish the main idea and system | `sw-chinese-opera-qupai` (opening stance, zaju branch / chuanqi branch) + `sw-premise-theme` | One person, one event, one sentence; number of 折 or 出; who holds the singing privilege (zaju) or how the 副末开场 (fùmò kāichǎng) is written (chuanqi) | Singing privilege = protagonist privilege holds; 题目正名 (tímù zhèngmíng) / 副末开场 exists |
| Q2 | Modes and staging | `sw-chinese-opera-qupai` (modes and suites, staging and plot) | Intended mode and suite form for each 折/出; staging table (hot/cold, short transitional scenes, use of Northern and Southern tunes) | One 折, one mode, one rhyme (zaju); the staging-alternation law passes; the division of labor between Northern and Southern tunes can be justified |
| Q3 | Characters and role types | `sw-chinese-opera-qupai` (four colors and four qi) + `sw-character-conflict` | Character table with role types and color-qi classification | 净 and 丑 have structural functions, not merely comic relief |
| Q4 | Tune-filling | `sw-chinese-opera-qupai` (tune-filling method) + the qupai table in `reference.md` | Qupai table (act / qupai / 务头 (wùtóu) line / rhyme); fix the 务头 before filling each tune | Metrical rules follow the score (or note the modern "zero gold, broken jade" route); at least half of the forty prohibitions pass |
| Q5 | First draft | `sw-chinese-opera-qupai` (speech-to-song seam, 帮腔 (bāngqiāng)) + `sw-dialogue` + `sw-chinese-opera-qupai-cases` | Script (song / speech / stage cues / 帮腔) | The spoken line before each tune introduces its first line; the table of famous works' metrical violations has been checked |
| Q6 | Revision | `sw-chinese-opera-qupai` (adaptation and rewriting, diagnostic checklist) | Revision record | The diagnostic checklist is complete; the three outcomes of adaptation have been compared (metrical correctness destroying the writing is a common failure) |

**Film/TV format skills not named in the two tables in this section (such as `sw-format-adaptation`) do not enter Chinese-opera projects; if you want to use one, first check the medium-boundary table in the corresponding opera skill.**

**One-off delivery** (writing one aria, revising one 折) does not build a bible; go directly to the relevant section of the corresponding skill.

---

## 4. Minimum Action Per Stage

You do not need to read the entire corresponding skill. At each stage, first read that skill's "Workflow" and "Diagnostic Checklist" sections; read the specific chapter when you need a method, and read reference.md when you need examples.

**Stage 1:** Follow the 12 steps in `sw-premise-theme` Section 12; write the output into the "Premise and Theme" section of the bible. If the user supplies external material such as a song, painting, or news story, first take only the narrative skeleton and images; invent the numbers, names, and sentences separately.

**Stage 2:** Fix the ending first; then convert the BS2 page numbers according to the target page count (scale the 110-page table proportionally: theme 5%, catalyst 11%, act two 23%, midpoint 50%, all is lost 68%, act three 77%); fill in the page table; write "what false impression the midpoint is and what opposite 'all is lost' is."

**Stage 3:** Fill one row of the three-dimensional table for each major character; separately write "what the unity-of-opposites binding object is, and whose which trait must die to break it"; give the opponent at least one knife; list the protagonist's shackles.

**Stage 4:** One row per scene in the step outline: `scene number | interior/exterior · location · day/night | one sentence | value at stake start → end | structural position`; then run "what happens if I delete it" and delete scenes whose value does not change.

**Stage 5:** After writing each day, update the "Progress" line in the bible (page count, which scene you have reached); when you find a design flaw, do not force a fix in the draft — go back to the bible, change the design, then change the draft.

**Stage 6:** Turn the questions in the five diagnostic checklists into a list of revision targets and cross them off one by one; do act two first, then dialogue, then format.

**Stage 7:** Generate the logline and one-page synopsis directly from the "Premise and Theme" section of the bible; run the PROBLEM seven elements.

---

## 5. How to Use the Passing Standards

- The standards are **suggested thresholds**, not hard blockers. If the user wants to skip a step, skip it, but mark "(skipped Stage 3 character table)" next to "Current Stage" in the bible and give one reminder before entering Stage 5.
- For the AI itself: at the end of each stage, ask yourself the questions in that skill's diagnostic checklist, and write failed items into the bible rather than silently letting them pass.
- Quantify everything quantifiable in the passing standards (page count, card count, character count, number of question marks).
- **The client's format requirements take precedence over any skill's house style.** If the user or commissioning party gives a page count, word count, columns, template, or episode count, follow theirs; the house styles in the skills (the three parts of an episode outline, the row format of a step outline, the field table of a document) are **defaults**, used only to fill blanks the other party has not specified. When they conflict, compress the house style rather than exceed the format, and save an expanded version separately for your own use. **Do not deliver a document that fails the client's specification just to fill in every field the skill requires.**

---

## 6. Subagents and Parallelism

- **Do not** split stages across different agents: premise, structure, and character are one body; splitting them creates contradictions and loses creative context. The main line always stays in one session.
- Two kinds of work **can** run in parallel:
  1. Multi-angle reading in Stage 6: assign one read-only agent each to structure diagnosis, character diagnosis, dialogue diagnosis, and scene diagnosis, run the checklists, and collect the results into one revision-target table.
  2. Large-scale retrieval: when you need a specific example from a reference.md or a scene-by-scene table for a work, send an agent to read it and bring back only the conclusions, avoiding context bloat in the main line.
- Parallel agents read only the bible and the draft; they do not modify the bible. Changes are summarized by the main line and then written in.

---

## 6.2 Output Language and Terminology

The original skill bodies were written in Chinese, and **parallel translations are not maintained for every language** — this English edition is one such translation; see the "Multilingual Support" section of the README. The language layer is handled by the following three rules, which apply to all sw-* skills.

1. **Output language = the language of the question.** If the user asks in English, Japanese, Korean, or French, deliver in that language; the original Chinese body does not affect the output language. If the user explicitly specifies a language, follow the specification ("write this outline version in English").
2. **Anchor terms back to their originals; do not invent translations.** Most terms in this line of work were originally English (logline, act out, beat sheet, showrunner); the Chinese book renderings "计程绳" (jìchéng shéng), "出幕" (chūmù), and "剧目管理人" (jùmù guǎnlǐrén) are translations. When outputting in a language other than Chinese, use the **English original** for every concept listed in [terms.md](terms.md); for concepts not in the table, first determine which language the original belongs to and anchor to it; do not silently invent.
3. **Words with no equivalent keep the original term + a one-line explanation.** Mainland-Chinese-specific terms (戏眼 (xìyǎn), 扣子 (kòuzi), 分集梗概 (fēnjí gěnggài), 备案公示 (bèi'àn gōngshì)) and Japanese terms (柱 (hashira), ト書き (tosho), 決定稿 (ketteikō)) are not forced into translation in any language; write them in forms such as `戏眼 (xìyǎn — the one-line core attraction of an episode)`.

**The script body itself is separate:** the script must be written in the language of the work, and the format chosen according to `sw-format-adaptation` (English drafts use spec/Fountain, Chinese drafts use the numbered-scene system, Japanese drafts use 柱・ト書き). It is normal for a user to discuss a Chinese script in English — **discuss in English, but keep the script body in Chinese**; do not change the work's language just because the conversation language changed.

---

## 6.3 Division of Labor Between Playwright and Director

The rules for the period after delivery come from Luo Huaizhen, "The Awakening of the Contemporary Chinese Opera Playwright-Director," pp. 0120–0125.

1. When the playwright puts down the pen, the form has already been born, but it is flat; what makes it three-dimensional is the director (p. 0120).
2. If the director's style matches the script's direction, cooperate; if it runs completely counter and exists only to test the director's own form, "decline early" (p. 0120).
3. Accepted revision notes should be **implemented by the playwright personally**, not farmed out to a ghostwriter (p. 0121); the consequence of not doing so is Chen Xiting's authorship lawsuit over *Dream of the Red Chamber* (pp. 0121–0122).
4. The bottom line of the second creation is **accuracy**: it may discover and present the script's spirit, but it may not slash and reinterpret at will (p. 0121).
5. Collaboration is **multiplication**, not subtraction, and not simple addition (p. 0122).
6. The reason the playwright does not also direct: directing one's own work can only copy the text and eliminates the possibility of creating it a second time (p. 0123).
7. Choose a director by four criteria: accurate interpretation, ability to offer constructive notes, professionalism, and control of the rehearsal room; "arrogance" is not an obstacle, but constant accommodation and indecision are disasters (pp. 0122–0123).

**Changeable / unchangeable** (four versions of *Xishi Returns to Yue*, pp. 0123–0124):

| Unchangeable | Changeable |
|---|---|
| Theme, framework | Rhymes |
| Relationships among major characters | Addition or removal of scenes |
| Basic dramatic plot | Treatment of the opening and ending, overall style (stylized / realistic) |

One criterion: **the literary spirit is unwavering.** This section applies equally to the Chinese-opera X/Q tables and the film/TV stage table.

---

## 7. Anti-Patterns

- Jumping straight from an idea to writing the script (a "counterfeit treatment").
- Rewriting the bible from scratch every session, or ignoring "Decided Decisions" and reopening the premise.
- Stuffing all reasoning into the bible so that it cannot be read through next time.
- Asking the user ten questions at once; infer and fill in first, mark "(to be confirmed)," and let the user correct it.
- Letting the "passing standards" become a reason to refuse to continue.
- Splitting the stages across subagents.
- Answering an English/Japanese/Korean/French question in Chinese because the skill body is Chinese; or, conversely, changing a Chinese script body into English because the conversation language is English.
- Inventing a translation for a concept whose original term already exists in terms.md.

---

## 8. Self-Check

1. Is there a `story-bible.md` in the current directory? Have you read "Current Stage / Decided Decisions / Decision Log"?
2. Did this session advance at least one stage deliverable and write it back?
3. Can the bible still be read in one sitting?
4. Did you change an established decision without logging it?
5. Did you write "Next step:" at the end?
6. Does the output language match the question language? Did you anchor terms back to the originals in terms.md? Has the script body's language been dragged off course by the conversation language?
