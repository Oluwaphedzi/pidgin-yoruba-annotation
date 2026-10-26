# Pidgin and Yoruba Dataset Annotation

**Oluwafeyikemi Dahunsi**
AI Data Evaluator | LLM Response Reviewer | Yoruba, English, Korean & Nigerian Pidgin

Lagos, Nigeria | [Email](mailto:dahunsioluwafeyikemi@gmail.com) | [LinkedIn](https://linkedin.com/in/oluwafeyikemi-dahunsi)

---

## Project Overview

Nigerian Pidgin and Yoruba are under-represented in the text that language models learn from. This portfolio project shows how I design a label schema and annotation guidelines for conversational text in these two languages, and how I apply them to real-sounding sentences.

It demonstrates my method for multilingual data annotation and linguistic quality assurance, including code-switching, Yoruba tone marks, register, sarcasm and privacy. It includes a 14-row labeled sample.

> **Sample work:** Every sentence below was written for this portfolio. The label schema and guidelines are my own demonstration, not a client's proprietary guide.

---

## Label Schema

| Field | Values | Rule |
| --- | --- | --- |
| `language` | yo, pcm, en, mixed | Use **mixed** when two languages appear in one sentence, and name the pair in `note`. |
| `intent` | greeting, request, question, complaint, apology, statement, farewell | Pick the main purpose of the speaker, one value. |
| `register` | formal, informal | Yoruba plural *Ẹ* to one person signals respect, so label formal. If the addressee is unknown, flag `unclear`. |
| `sentiment` | positive, neutral, negative | Judge the speaker's feeling, not the topic. |
| `flag` | none, sensitive, unclear | Use **sensitive** for politics, health or religion. Use **unclear** if two readings are equally likely (for example, possible sarcasm). |
| `note` | free text (optional) | Record missing tone marks, the language pair for mixed rows, and the reason for any borderline label. |

## Annotation Rules

- Do not correct spelling in the text. Label what is written, because informal spelling is training signal.
- Keep Yoruba tone marks and under-dots exactly as the writer typed them. If marks are missing, record that in `note`, not in the text.
- Pidgin has no single standard spelling. *Dey* and *de* are treated as the same word.
- Sarcasm is labeled by the speaker's real feeling and flagged `unclear` if it cannot be told from the sentence alone.
- Phrases that calm the listener, such as "no vex", are labeled `apology` when the speaker is trying to settle a tense moment.
- Replace names, phone numbers and addresses with placeholders (`[NAME]`, `[PHONE]`, `[ADDRESS]`) before the text enters the dataset. Placeholders are the only edits allowed to the text.

---

## Labeled Sample

Fourteen rows: seven Nigerian Pidgin, five Yoruba, one code-switched and one Nigerian English.

| # | Text | Lang | Intent | Register | Sentiment | Flag |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | How far? You don chop? | pcm | greeting | informal | positive | none |
| 2 | Abeg, help me carry this load. | pcm | request | informal | neutral | none |
| 3 | Wetin dey happen for road? Traffic too much! | pcm | complaint | informal | negative | none |
| 4 | I no go gree for dem o. | pcm | statement | informal | negative | none |
| 5 | Dis government no dey try at all. | pcm | complaint | informal | negative | sensitive |
| 6 | Oga, na so e be o. No vex. | pcm | apology | informal | neutral | none |
| 7 | Ẹ kú àárọ̀, báwo ni? | yo | greeting | formal | positive | none |
| 8 | Mo fẹ́ ra ìrẹsì. | yo | request | informal | neutral | none |
| 9 | Ọmọ mi ń ṣàìsàn, mo nílò dókítà. | yo | request | informal | negative | sensitive |
| 10 | Ṣé o ti jẹun? | yo | question | informal | positive | none |
| 11 | Ó dàbọ̀, a ó tún rí ara wa. | yo | farewell | informal | positive | none |
| 12 | Mo ti pay owó ilé, ṣùgbọ́n landlord ò tí ì fún mi ní receipt. | mixed | complaint | informal | negative | none |
| 13 | Na you sabi. | pcm | statement | informal | neutral | unclear |
| 14 | Good afternoon, Ma. Please, can I get the account number for the transfer? | en | request | formal | neutral | none |

### Reasoning on the Hard Rows

- **Row 5.** A complaint about government is a political topic, so it gets the `sensitive` flag even though the language is plain.
- **Row 6.** "No vex" asks the listener not to be angry. I label it `apology` with neutral sentiment, since the speaker is calming a situation. This is a borderline case, so it is covered by its own rule in the annotation rules.
- **Row 7.** The plural *Ẹ* used toward one person is a respect marker, so register is formal. This assumes the addressee is a single person, such as an elder. With an unknown or group addressee, the row would be flagged `unclear`.
- **Row 9.** The intent is a request for help. A sick child makes it a health topic, so it is flagged `sensitive`.
- **Row 12.** Yoruba sentence structure with an English verb and two English nouns. Language is `mixed`, and `note` records the pair as Yoruba and English.
- **Row 13.** "Na you sabi" can be genuine praise ("you know best") or mockery. The sentence alone does not settle it, so it is flagged `unclear` and sentiment is left neutral.
- **Row 14.** Nigerian English with a respectful "Ma" and "Please", so register is formal.

---

## Quality Checks

| Check | How |
| --- | --- |
| Consistency | Re-label 10% of rows a day later and compare with the first pass. |
| Disagreement | Rows where two labelers differ go to a short written resolution, and the rule is added to this guide. |
| Agreement metrics | Report percent agreement and Cohen's kappa for each field. These are the method targets for a full dataset, not results measured on this 14-row sample. |
| Privacy | Scan every row for names, numbers and addresses before export. |

---
*Sample portfolio project. Schema and sentences created for demonstration.*
