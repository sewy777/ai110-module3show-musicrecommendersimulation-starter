# Reflection: Profile Comparison Notes

These are my notes comparing how the recommender behaved for different user profiles.
Written for someone who doesn't code — just explaining what changed and why it makes sense.

---

## High-Energy Pop vs. Chill Lofi

These two profiles are basically opposites and the recommender handled them really differently, which is a good sign. High-Energy Pop got Sunrise City and Gym Hero at the top — both are pop songs with high energy. Chill Lofi got Library Rain and Midnight Coding, which are both slow, quiet, study-type tracks. The system clearly separated these two worlds correctly. The interesting part is that neither profile's top results ever showed up in the other's list, which means the genre + energy combo is doing its job when there's a clear match available.

---

## High-Energy Pop vs. Deep Intense Rock

Both profiles want high energy, but the genre and mood are different — one wants happy pop, the other wants intense rock. What's interesting is that "Gym Hero" (intense pop) appeared in the High-Energy Pop top 5 at #2 even though its mood is "intense," not "happy." That's because the genre match (+2.0) was strong enough to pull it up even without the mood bonus. Meanwhile, Deep Intense Rock correctly put Storm Runner first because it matched genre, mood, AND energy at the same time. This comparison shows that when genre aligns perfectly with mood AND energy, you get near-perfect scores — but when they conflict (like Gym Hero being intense instead of happy), the song still ranks high just from the genre bonus alone.

---

## Deep Intense Rock vs. High-Energy Classical (adversarial)

This comparison is where things get weird. Deep Intense Rock found a real match (Storm Runner) and ranked it perfectly. But High-Energy Classical had no good match in the catalog — there's only one classical song and it's peaceful and quiet, not high-energy at all. The system still ranked it first (Morning Mist, score 2.27) just because it was the only genre match. Second place was actually Bass Drop Heaven, an EDM track, because it matched the "euphoric" mood and had high energy. In a real recommender, the system would probably recognize that the user's classical + high-energy request doesn't have a great answer and maybe suggest they explore a new genre. Our system can't do that — it just hands you the closest thing it has, even if it's not close at all.

---

## Chill Lofi vs. Sad EDM (adversarial)

Chill Lofi is a profile the system handles well — there are three lofi songs in the catalog and they all have low energy and calm moods, so they match up naturally. Sad EDM is the opposite problem: our catalog only has one EDM song and it's tagged as "euphoric," not "sad." The system gave Bass Drop Heaven a 2.95 score (genre match + energy similarity) but completely missed on mood. The rest of the top 5 for Sad EDM were just high-energy songs with no mood or genre connection at all — Storm Runner, Gym Hero, Iron Will. It's a bit funny honestly, because someone looking for sad EDM got recommended a metal song and a pop workout track. This shows that when a user's mood preference doesn't exist in the catalog, the mood score becomes zero for everything and the system just falls back to ranking by genre + energy.

---

## Weight Shift Experiment: Halved Genre, Doubled Energy

When I changed the genre weight from +2.0 to +1.0 and doubled the energy similarity, the top results mostly stayed the same for profiles that had clear genre matches (the best song still won because it matched everything). But the middle of the ranking shifted noticeably. For the High-Energy Pop profile, Rooftop Lights jumped from #3 to a much closer second place — it doesn't match the genre but it has high energy and a happy mood, so those two things together became more competitive once genre stopped dominating. The experiment showed that the original weights make genre feel almost like a hard filter rather than just one factor among many.
