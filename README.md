# AES2025-materials
This repository will host supplementary materials related to my AES paper A Scalable Two-Stage Automatic Mixing System Integrating Machine Learning and Domain Knowledge. Materials will be updated after publication.
Perfect 👍 — here’s your full version as a clean Markdown table,
fully GitHub-compatible and optimized for README or dataset documentation.
All formatting (bold, italics, line breaks) will render correctly on GitHub.

⸻

🎚️ Audio File States in the Music Mixing Process (Standard Terminology Reference)

Stage	Description (Chinese)	✅ Recommended Standard English Term	💬 Common Alternatives / Notes	✅ Recommended Dataset / File Naming Examples	📘 Explanation / Use Case
1️⃣	混音前音轨	Raw Multitracks	Dry stems, Unprocessed stems, Isolated tracks	song001_track_vocal_raw.wavsong001_track_guitar_raw.wav	Independent tracks recorded before any processing. Typically microphone-level recordings (e.g., vocal.wav, guitar.wav).
2️⃣	混音后音轨（与原始音轨一一对应）	Processed Multitracks	Track-level renders, Effect-applied tracks	song001_track_vocal_processed.wavsong001_track_guitar_processed.wav	Each original recording track is independently rendered after applying its dedicated mixing chain (EQ, compression, reverb, etc.). Maintains strict one-to-one correspondence with the Raw Multitracks.
3️⃣	分组混音轨（如鼓组、人声组等的子混音）	Processed Stems	Group stems, Stem bounces, Submix stems	song001_stem_drums.wavsong001_stem_vocals.wavsong001_stem_fx.wav	Multiple Processed Multitracks are grouped and summed by instrument or function into unique audio files for each group.
4️⃣	混缩结果（立体声 / 多声道）	Final Mixdown	Stereo mix, 5.1 mix, Dolby Atmos mix, Immersive mix	song001_mix_stereo.wavsong001_mix_5.1.wavsong001_mix_atmos.wav	All stems are summed through the mixing console into a single master track. This file is delivered to the mastering engineer, usually exported as a 24-bit WAV.
5️⃣	母带后成品	Mastered Version	Mastered mix, Final master, Distribution master, MMM (China)	song001_master_stereo.wavsong001_master_atmos.wav	The final version after the mastering engineer applies EQ, limiting, loudness, and encoding optimization. Used for release, evaluation, or distribution—the final stage before publication.
—	对照参考	Reference Mix / Commercial Master	—	reference_mix_song001.wavcommercial_master_song001.wav	The target audio used for perceptual evaluation or mixing style-transfer tasks. May serve as a reference for system training or subjective listening tests.


⸻

🎧 Audio Production Workflow Diagram (Recording → Mixing → Mastering → Distribution)

[1️⃣ Raw Multitracks]
     ↓  (Track-level mixing and processing)
[2️⃣ Processed Multitracks]
     ↓  (Grouped by instrument or functional category)
[3️⃣ Processed Stems]
     ↓  (Summed and exported as a single mix)
[4️⃣ Final Mixdown]
     ↓  (Mastering stage: EQ / Limiting / Loudness optimization)
[5️⃣ Mastered Version]
     ↓
[Commercial Release / Reference Mix]


⸻

✅ Summary
	•	Raw Multitracks → Original recordings before mixing
	•	Processed Multitracks → One-to-one processed versions of each track
	•	Processed Stems → Grouped submixes by instrument or role
	•	Final Mixdown → Complete stereo or spatial mix export
	•	Mastered Version → Loudness-optimized, distribution-ready product
	•	Reference Mix → Target for style-transfer or perceptual evaluation

⸻

Would you like me to make a matching “Dataset hierarchy diagram” (folder structure tree showing how these files could be organized in /data/)? It would make your README even more practical.
