# 🎵 Music Recommender Simulation

## Project Summary

My version of this project builds a content-based music recommender that scores songs against a user's taste profile. It uses three features — genre, mood, and energy — to calculate a score for each song and returns the top 5 matches with plain-language explanations. I tested it with three different user profiles and ran an experiment changing the energy weight to see how it affected results.

---

## How The System Works

Each song in the catalog has these features: genre, mood, energy (0.0–1.0), tempo_bpm, valence, danceability, and acousticness.

The UserProfile stores: favorite_genre, favorite_mood, target_energy, and likes_acoustic.

**Algorithm Recipe:**
- Genre match: +2.0 points
- Mood match: +1.0 points
- Energy similarity: up to +1.0 points using `1 - abs(song_energy - target_energy)`

Songs are scored individually, sorted highest to lowest, and the top 5 are returned with reasons explaining each score.

---

## Getting Started

### Setup

1. Create a virtual environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

2. Install dependencies:

```bash
pip install -r requirements.txt
```

3. Run the app:

```bash
python -m src.main
```

### Running Tests

```bash
pytest
```

---

## Experiments You Tried

- **Baseline:** Genre match (+2.0), mood match (+1.0), energy similarity (0–1.0). Worked well for pop and lofi profiles but poorly for rock since only one rock song existed in the catalog.
- **2x Energy Weight:** Changed energy multiplier from 1.0 to 2.0. Scores increased but song rankings stayed identical, showing that genre dominates the scoring no matter what.
- **Key finding:** The Intense Rock profile exposed a filter bubble — when a genre is underrepresented in the dataset, the recommender fails that user regardless of the weights.

---

## Limitations and Risks

- Only works on a tiny catalog of 10 songs
- Genre is worth twice as much as mood, creating a strong bias toward genre matching
- Rock and other minority genres in the dataset get much worse recommendations
- Does not consider tempo, lyrics, or listening history
- Cannot learn or improve from user feedback

---

## Reflection

Building this recommender taught me that turning data into predictions is really just math with opinions baked in. Every weight I assigned like making genre worth +2 points and mood worth only +1 was a design choice that directly shaped what the system recommended. The system doesn't understand music at all. It just compares numbers. What surprised me most was how a single number change (doubling the energy weight) didn't even change the song rankings  genre was so dominant it didn't matter. That made me realize how easy it is to accidentally make a biased system just by picking one feature over another without thinking about it.

Bias in a system like this can sneak in from two places: the weights and the data. My genre weight being twice as strong as mood means users whose favorite genre isn't well represented in the catalog get much worse recommendations than pop or lofi fans. If this were a real product, that would mean certain groups of users consistently get a worse experience just because of how I built the math. Real platforms have the same problem at a much larger scale their training data reflects whoever was already using the platform, which means new or niche tastes get underserved. Building even this tiny version made that very concrete for me.