# Hungarian 1000: the most frequent verbs

The 1000 most frequent Hungarian verbs, each in one short, natural example sentence,
with English and Russian translations and audio. It comes as a ready-to-study Anki
deck, an open dataset (JSON / CSV / XLSX), and audio packs.

Cards are ordered by frequency, so #1 is the most common verb and you pick up the
most useful words first.

*The example sentences and translations were drafted with an LLM and then checked over
several review passes, with tricky grammar verified against dictionaries. The audio is
text-to-speech. There is more on all of this further down.*

## Download

Everything is on the [Releases page](https://github.com/iperx/hungarian-1000-verbs/releases/latest):

| File | What it is |
|---|---|
| `hu_verbs_1000_en.apkg` | Anki deck, Hungarian and English |
| `hu_verbs_1000_ru.apkg` | Anki deck, Hungarian and Russian |
| `audio_male_1000.zip` | 1000 sentence recordings, male voice (Tamás) |
| `audio_female_1000.zip` | 1000 sentence recordings, female voice (Noémi) |
| `*_gapped.mp3`, `*_gapped_2s.mp3` | Full passive-listening tracks with shorter and longer pauses between sentences, male and female |

The dataset (`data/`) and the card previews (`preview/`) are in this repo directly.

To use a deck, open Anki and choose File then Import, and pick the `.apkg`. Everything,
including the audio, is bundled inside.

You can also see the card design without installing anything:
[English cards](https://iperx.github.io/hungarian-1000-verbs/preview/card_preview_en.html)
and [Russian cards](https://iperx.github.io/hungarian-1000-verbs/preview/card_preview_ru.html).

## Why this exists, and the method behind it

I have been into Hungarian for a while, and I am still after a way to study it that
really clicks. There is not much modern material for the language, and understanding
most podcasts and videos is still out of reach for me, so I wanted something convenient
to practice with to get going. Then I came across
[Natural Language Learning](https://www.youtube.com/@NaturalLanguageLearning) and its
video ["Learn 2000 Words in 7 Days and Understand 90% of Any Language"](https://youtu.be/etywD4c7S6U),
and it made sense. The gist:

- **Verbs first.** A verb carries the action, the meaning of a sentence, so verbs are
  the highest-leverage words for comprehension.
- **Frequency order (Zipf's law).** The most common words show up far more often than
  the rest. By the author's estimate the top 2000 verbs get you to about 90 percent
  comprehension, and even the first 1000 to around 80 percent.
- **Learn them inside example sentences.** A sentence teaches the verb and a lot of the
  surrounding vocabulary for free.
- **Listen a lot.** Play the sentences on repeat while walking, commuting, or working
  out. Repetition is the engine.
- **Two passes.** First read while listening, to lock in the meaning. Then do active
  recall: read the translation and try to say the sentence out loud. Later you bridge to
  real speech by going back and forth between your easy sentences and native podcasts.

That last bridge, easing from your own sentences into real audio, is the part I believe
in most. It has worked for me with other languages before.

What I did differently:

- **I made the data myself.** The video explains the method but does not include the
  sentences, and nothing ready-made existed for Hungarian, so I generated the whole
  dataset along these lines.
- **Just the first 1000 verbs.** That is already around 80 percent comprehension by the
  author's estimate, so it stays focused and is actually finishable.
- **Sentences in the same spirit:** short, lifelike, one verb each, in a natural
  conjugated form and with the right verb pattern, meaning the case the verb takes (vonzat).
- **Enriched with the 356 most useful high-frequency words.** Beyond the verb, each
  sentence weaves in common adverbs, pronouns, and connectives (early/late,
  together/alone, sometimes/always/never, someone/somewhere) drawn from a 356-word pool,
  so the deck quietly teaches far more than 1000 words.
- **Built for the method.** The three card types map straight onto it: Listening (read
  while hearing), Recall (active recall back into Hungarian), and Pure audio (train your
  ear). The full listening tracks cover the "listen all day" part.

## What's in a card

Each verb is one note with three card types, so you drill different skills:

1. **Listening:** hear and read the Hungarian sentence, then recall the meaning.
2. **Recall:** see the meaning, then produce the Hungarian sentence.
3. **Pure audio:** listen only, then reveal the sentence and translation.

On every card:

- the exact conjugated verb form is highlighted in the sentence (separated preverbs
  like "teszek fel" are highlighted as one unit);
- one Play button, with each note bound to a male or female voice (roughly half and half
  across the deck) and native autoplay;
- the infinitive and a translation of the verb and the sentence;
- a small register note for the non-neutral verbs (colloquial, vulgar, or violent).

## The dataset (for developers)

`data/hu_verbs_1000.json` is a single array of 1000 objects:

```json
{
  "id": "0001",
  "rank": 1,
  "verb": "van",
  "infinitive": "lenni",
  "register": "neutral",
  "sentence_hu": "Ő most az iskolában van.",
  "verb_form_used": "van",
  "audio": { "male": "0001_van_m.mp3", "female": "0001_van_f.mp3" },
  "translations": {
    "ru": { "verb": "быть, находиться", "sentence": "Он сейчас в школе." },
    "en": { "verb": "to be", "sentence": "She is at school right now." }
  }
}
```

- `rank`: frequency rank, where 1 is the most frequent.
- `register`: one of neutral, colloquial, vulgar, violent.
- `verb_form_used`: the exact form appearing in `sentence_hu`, handy for highlighting.
- `audio`: filenames inside the audio packs.

The same data is also there as `data/hu_verbs_1000_{en,ru}.csv` and `.xlsx` (UTF-8 with
a BOM, friendly to Google Sheets).

## How it was made

- **Verb list and order:** verbs ranked by frequency from OpenSubtitles data, lemmatized
  and POS-tagged with [HuSpaCy](https://github.com/huspacy/huspacy) (`hu_core_news_md`),
  then curated.
- **Sentences and translations:** drafted with a large language model (Anthropic Claude),
  kept to short, lifelike A1-A2 sentences with a pronoun subject and the correct verb
  pattern (vonzat).
- **Validation:** structural checks (the verb is actually present) plus several
  independent review passes per sentence, with debatable grammar cross-checked against
  dictionaries (Wiktionary and [Wikiszótár.hu](https://wikiszotar.hu)).
- **Audio:** text-to-speech via [edge-tts](https://github.com/rany2/edge-tts) with the
  Microsoft Hungarian voices Tamás (male) and Noémi (female).

Full notes and the license of every source and tool are in [CREDITS.md](CREDITS.md).

## License

The dataset (the example sentences, the translations, and their selection and
arrangement) is licensed [CC BY 4.0](LICENSE), so it is free to use and adapt with
attribution.

The audio is text-to-speech made with Microsoft voices and provided for free
educational use. The frequency data comes from OpenSubtitles. See [CREDITS.md](CREDITS.md).

## По-русски

Я сам давно интересуюсь венгерским и ищу удобный подход к его изучению. Современных
учебных материалов по венгерскому не так много, а понимать большинство подкастов и
видео ещё рано. Нужна удобная практика для старта.

**Вдохновился** каналом [Natural Language Learning](https://www.youtube.com/@NaturalLanguageLearning)
и, в частности, видео ["Learn 2000 Words in 7 Days..."](https://youtu.be/etywD4c7S6U).
Идея показалась простой и логичной: глаголы - самые важные для понимания слова, поэтому
учить их стоит по частотности (сначала самые частые, по закону Ципфа), в
примерах-предложениях, и очень много слушать. Учёба в два прохода: сначала читать и
слушать одновременно, потом активно вспоминать и проговаривать вслух. А дальше
открывается путь к пониманию настоящей речи - тот самый переход к подкастам, в который я
верю и который уже помогал мне с другими языками.

**Что я сделал иначе:** взял **только первую тысячу глаголов** - по словам автора, это
уже около 80 процентов понимания (а все 2000 - около 90), так что получается фокусно и
реально дойти до конца. Готовых предложений автор не прикладывает, поэтому данные я
собрал сам, в том же духе, и **обогатил их 356 самыми полезными частотными словами**:
наречия, местоимения, союзы (рано/поздно, вместе/один, иногда/всегда/никогда,
кто-то/где-то). Так что колода попутно учит куда больше тысячи слов. Три типа карточек
как раз ложатся на метод: аудирование, активное припоминание и чистое аудио, плюс полные
аудиодорожки, чтобы слушать весь день.

**Что внутри:** 1000 глаголов, каждый в коротком естественном предложении, с переводами
(английский и русский) и озвучкой. Готовая колода Anki, открытый датасет (JSON / CSV /
XLSX) и аудио-паки. На карточках: подсветка нужной формы глагола, одна кнопка Play
(мужской или женский голос, примерно поровну по колоде) и пометки регистра. Карточки
идут по частотности, #1 самый частый. Источники и лицензии - в [CREDITS.md](CREDITS.md).
