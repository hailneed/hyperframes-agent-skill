---
name: voiceover
description: Adding AI-generated voiceover to HyperFrames compositions using ElevenLabs TTS
metadata:
  tags: voiceover, audio, elevenlabs, tts, speech, ai
---

# Adding AI voiceover to a HyperFrames composition

Use ElevenLabs TTS to generate speech audio per scene, then reference the MP3 files as `<audio>` clips.

## Prerequisites

This guide uses **ElevenLabs** as the TTS provider (`ELEVENLABS_API_KEY` environment variable).

If the user has not specified a TTS provider, recommend ElevenLabs and ask for their API key.

## Generating audio with ElevenLabs

Create a script that calls the ElevenLabs API for each scene and writes MP3 files to `assets/`:

```ts
// generate-voiceover.ts
import { writeFileSync, mkdirSync } from 'node:fs';

const VOICE_ID = 'EXAVITQu4vr4xnSDxMaL'; // Rachel
const scenes = [
  { id: 'intro',   text: 'Welcome to our product showcase.' },
  { id: 'product', text: 'Introducing the all-new AirMax Pro.' },
  { id: 'cta',     text: 'Order yours today at our website.' },
];

mkdirSync('assets/voiceover', { recursive: true });

for (const scene of scenes) {
  const res = await fetch(`https://api.elevenlabs.io/v1/text-to-speech/${VOICE_ID}`, {
    method: 'POST',
    headers: {
      'xi-api-key': process.env.ELEVENLABS_API_KEY!,
      'Content-Type': 'application/json',
      Accept: 'audio/mpeg',
    },
    body: JSON.stringify({
      text: scene.text,
      model_id: 'eleven_multilingual_v2',
      voice_settings: { stability: 0.5, similarity_boost: 0.75, style: 0.3 },
    }),
  });
  writeFileSync(`assets/voiceover/${scene.id}.mp3`, Buffer.from(await res.arrayBuffer()));
  console.log(`Generated: assets/voiceover/${scene.id}.mp3`);
}
```

Run it:

```bash
ELEVENLABS_API_KEY=your_key node --strip-types generate-voiceover.ts
```

## Getting audio duration

Use `ffprobe` (bundled with FFmpeg) to measure each generated file:

```ts
import { execSync } from 'node:child_process';

function getAudioDuration(filePath: string): number {
  const output = execSync(
    `ffprobe -v error -show_entries format=duration -of csv=p=0 "${filePath}"`
  ).toString().trim();
  return parseFloat(output);
}

const durations = {
  intro:   getAudioDuration('assets/voiceover/intro.mp3'),
  product: getAudioDuration('assets/voiceover/product.mp3'),
  cta:     getAudioDuration('assets/voiceover/cta.mp3'),
};
console.log(durations);
// e.g. { intro: 2.4, product: 3.1, cta: 2.0 }
```

## Using voiceover in the composition

Reference generated MP3 files as `<audio>` clips. Calculate `data-start` from cumulative durations:

```html
<!-- Intro scene: 0s – 2.4s -->
<video id="s1-bg"  class="clip" data-start="0"   data-duration="2.4" data-track-index="0" src="intro.mp4"   muted></video>
<audio id="s1-vo"  class="clip" data-start="0"   data-duration="2.4" data-track-index="10" data-volume="1.0" src="assets/voiceover/intro.mp3"></audio>

<!-- Product scene: 2.4s – 5.5s -->
<video id="s2-bg"  class="clip" data-start="2.4" data-duration="3.1" data-track-index="0" src="product.mp4" muted></video>
<audio id="s2-vo"  class="clip" data-start="2.4" data-duration="3.1" data-track-index="10" data-volume="1.0" src="assets/voiceover/product.mp3"></audio>

<!-- CTA scene: 5.5s – 7.5s -->
<video id="s3-bg"  class="clip" data-start="5.5" data-duration="2.0" data-track-index="0" src="cta.mp4"     muted></video>
<audio id="s3-vo"  class="clip" data-start="5.5" data-duration="2.0" data-track-index="10" data-volume="1.0" src="assets/voiceover/cta.mp3"></audio>

<!-- Background music under everything -->
<audio id="music"  class="clip" data-start="0"   data-duration="7.5" data-track-index="9"  data-volume="0.15" src="assets/bg-music.mp3"></audio>
```

## Adjusting composition total duration

After generating voiceover, total duration = sum of all scene durations. Update video clip durations to match.

## Delaying voiceover start

Add a small offset to `data-start` for a natural pause after the visual cuts in:

```html
<!-- Visual appears at 2.4s, voice starts 0.3s later -->
<audio id="s2-vo" class="clip" data-start="2.7" data-duration="3.1" data-track-index="10" src="assets/voiceover/product.mp3"></audio>
```
