# Achernar Training Data (synthetic)

13,100 text-to-speech clips generated with the Google Achernar voice, paired
with the [LJSpeech](https://keithito.com/LJ-Speech-Dataset/) transcripts.
Published as the training corpus for an `en_US-achernar-medium` Piper voice.

## Please read: this audio is synthetic

**Every WAV in this repository is machine-generated speech.** None of it is a
human recording. It was produced by a neural text-to-speech system, not by
LibriVox volunteers and not by Linda Johnson, whose voice is the original
LJSpeech speaker.

This matters for how you use it:

- Do not present it as human speech, human voice data, or a voice-cloning
  sample. It is a TTS output, and it is labelled as one.
- Do not use it to evaluate or claim speech naturalness against human
  recordings without accounting for the synthetic origin.
- It is useful for training TTS acoustic models, for speaker/voice conversion
  research, and for pipeline development. It is not a substitute for a human
  corpus if your research depends on real human recordings.

## Contents

| Path | Description |
| --- | --- |
| `wav22/` | 13,100 WAV files, LJSpeech clip IDs (`LJ001-0001.wav`, ...) |
| `txt/` | 13,100 matching transcripts, one UTF-8 `.txt` per clip |
| `metadata.csv` | Piper training metadata, `filename\|text` per line |
| `LICENSE` | Public domain dedication (Unlicense) |

The 24 kHz masters and the resampling manifest used to build this corpus were
deliberately not published; only the training-ready 22.05 kHz audio is here.

## Statistics

| Property | Value |
| --- | --- |
| Clips | 13,100 |
| Total duration | 20.805 hours (1,651,518,540 samples) |
| Sample rate | 22,050 Hz (all files) |
| Channels | 1 (mono, all files) |
| Sample width | 16-bit PCM |
| Clip length min / median / max | 0.72 s / 5.84 s / 12.40 s |
| Clips shorter than 1 s | 5 |
| Clips longer than 10 s | 30 |
| File size range | 31,796 - 546,884 bytes |
| Transcript source | LJSpeech `text_normalized` |

The five sub-second and thirty over-ten-second clips are a natural consequence
of neural TTS pacing and differ slightly from the segmentation boundaries of
the original human recordings, which were cut on detected silence.

### Sample rate

Audio is 22,050 Hz to match Piper's `medium` quality tier directly. The Google
voice renders natively at 24 kHz, so the published audio was resampled to
22,050 Hz with a very-high-quality resampler. If you need a different rate,
resample from these files; do not expect to recover the 24 kHz originals from
this repository.

## Format

`metadata.csv` uses the `|` delimiter expected by `piper.train`:

```
LJ001-0001.wav|Printing, in the only sense with which ...
```

Transcripts are LJSpeech's **normalized** text: lower-cased, with numbers and
abbreviations spelled out. They are not the original book text, and they are
normalised for a speech engine rather than for reading.

## How this was built

1. Fetched all 13,100 LJSpeech `text_normalized` transcripts.
2. Synthesized each one with the Google Cloud Text-to-Speech voice
   `en-US-Chirp3-HD-Achernar` through a STAR synthesis endpoint, requesting
   24 kHz mono linear PCM. Transient upstream failures were retried until
   every clip was produced.
3. Verified the 24 kHz masters for format, clipping, silence, and duration
   outliers.
4. Resampled to 22,050 Hz for the Piper `medium` tier and wrote
   `metadata.csv`.

## Licensing and provenance

The underlying material is in the **public domain**, so this derivative carries
no restrictions:

- **Texts**: excerpts from seven non-fiction books published between 1884 and
  1964, all public domain.
- **Original LJSpeech audio**: recorded in 2016-17 by the LibriVox project
  (voice: Linda Johnson), public domain. Annotation and alignment by Keith Ito.
- The LJSpeech authors state: "This dataset is in the public domain in the US
  (and most likely other countries as well). There are no restrictions on its
  use." They ask only that it be used for good and not for evil.

The audio published here is a new synthetic rendering of those public-domain
texts. The public-domain status of the texts carries over to it.

### Citation

If you use this corpus in a publication, please cite LJSpeech, since you are
using its transcripts:

```bibtex
@misc{ljspeech17,
  author       = {Keith Ito and Linda Johnson},
  title        = {The LJ Speech Dataset},
  howpublished = {\url{https://keithito.com/LJ-Speech-Dataset/}},
  year         = {2017}
}
```

## Intended use

Training and evaluating text-to-speech and voice-conversion models; developing
and testing audio pipelines. See the LJSpeech terms above regarding use for
good and not evil.
