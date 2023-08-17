# Photo-Sequence-Optimization
You need to match vertical photos into "combined" photos. You need to arrange the combined/horizontal photos for maximum score.

# Problem statement:

You are given a list photos.
Each photo is either "horizontal" or "vertical".
Each photo has a list of tags.
If the photo is vertical, you will need to merge it with another vertical photo to form a combined photo. The combined photo will contain all the tags from both photos.
You will need to provide a sequence of combined and horizontal photos to that maximises the score of your solution.
The score of your solution is the sum of scores between all pairs of neighbours in your produced sequence.
# Score
The score between neighbouring combined/horizontal photos is the minimum of

tags found in both neighbours
tags found only in the first neighbour
tags found only in the second neighbour

# How the vertical photos are matched

Conducting a data analysis on the vertical photos, we see that there are signficant overlap in the number of tags between vertical photo pairs.
I needed to match the photos in the way that it minimise the amount of overlapping tags.
I avoid pairings that result in odd number of tags. This improved the solution my almost a thousand from 440k. This improved the result slightly, but adds 5 minutes to the computation time.
I try to pair pictures so that their tags combined is close to 20 (and even), the average. The hypothesis is that with a similar amount of tags, it is easier to find the next neighbour with the optimum score. This also require the increased computation time.

# How the photos are arranged

This is now a travelling salesman problem (TSP). Each node is one combined/horizontal photo. A score is assigned between each combination of combined/horizontal pairs, like how a distance is assigned between each location pairs in the traditional TSP. Instead of minimising distance in the traditional TSP, we maximise the score.
A greedy approach is used.
The greedy search starts from the combined/horizontal photos with the most number of tags. We do this until no more combined/horizontal photos are left.
We do not search in all the remaining photos. Instead of searching from all the remaining photo, we search among the remaining K=10000 photos.
We can also stop when we have obtained the maximum possible score, calculated from the number of tags of the preceding photo. This drastically sped up our computation time from 1 hour with K=10000 to 6 minutes.
