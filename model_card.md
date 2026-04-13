
# Model Card - Music Recommender Simulation

## 1. Model Name
VibeFinder 1.0

## 2. Intended Use
This system suggests 5 songs from a small catalog based on a user's preferred genre, mood, and energy level. It's built for a classroom project to understand how basic content-based recommendation works. It is not meant for real users or production use.

## 3. How It Works
Each song gets a score based on three things: whether its genre matches the user's favorite (+2 points), whether its mood matches (+1 point), and how close its energy level is to what the user wants (0 to 1 point). Songs are ranked from highest to lowest score and the top 5 are returned with reasons explaining why each one was picked.

## 4. Data
The dataset has 10 songs in data/songs.csv. Each song has a title, artist, genre, mood, energy (0.0 to 1.0), tempo, valence, danceability, and acousticness. The catalog is small and mostly pop and lofi, which means other genres like rock or jazz are underrepresented.

## 5. Strengths
The system works well when the catalog has songs that clearly match the user's genre and mood. For example, the Chill Lofi profile consistently returned accurate lofi songs at the top. It is also transparent — every recommendation comes with a clear reason explaining the score.

## 6. Limitations and Bias
Genre is worth twice as many points as mood, so the system heavily favors genre matches even when a song's mood or energy might be a better fit. The Intense Rock profile only found one actual rock song, so the remaining results were just pop songs with high energy. The small dataset also creates a filter bubble — if you don't like pop or lofi, the system struggles. The system also doesn't consider tempo, lyrics, or listening history at all.

## 7. Evaluation
I tested three user profiles: High-Energy Pop, Chill Lofi, and Intense Rock. The pop and lofi profiles returned results that felt accurate. The rock profile exposed a clear weakness — only one rock song existed in the catalog so the rest of the top 5 were unrelated genres. I also ran an experiment doubling the energy weight from 1.0 to 2.0. The song rankings stayed the same but scores increased. This showed that the order of results is mostly driven by genre, not energy.

## 8. Future Work
- Add more songs across more genres so underrepresented users get better results
- Add tempo as a scoring feature to better separate high-energy rock from high-energy pop
- Reduce the genre weight so mood and energy have more influence on the final ranking

## 9. Personal Reflection
The biggest thing I learned is that small weight differences completely change what a recommender feels like to use. I expected the system to feel smart, but it's really just math — genre match wins almost every time because it's worth the most points. Building this made me realize how easy it is to accidentally bake in bias just by choosing one number over another. Real platforms like Spotify probably have hundreds of these weights tuned over millions of users, which is what makes them feel so accurate. If I kept working on this I'd want to add more songs and experiment with making the weights adjustable by the user themselves.