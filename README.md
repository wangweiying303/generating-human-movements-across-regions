# generating-human-movements-across-regions
Here are some codes used to generate human movements with numpy. It is quite fast.


Data required: population and centroid of each administrative region.


The codes first parse the website "https://en.wikipedia.org/wiki/List_of_districts_of_Madhya_Pradesh" for the name and population of each district of Madhya Pradesh state in India.
The "OpenStreetMap" API was then used to get the boundary of each district and the distance between districts.


The codes follow some parts of this paper: Reference 1 https://www.sciencedirect.com/science/article/pii/S1877050916302216, but use matrix operations to make the generation much faster.
Applied gravity model and the EPR model (EPR model: Reference 2 https://www.nature.com/articles/nphys1760).


Important notice:
Different from References 1 & 2 (where waiting time follows P(Δt) ∼ Δt^(−1−β)*exp(−Δt/τ)), in my code, the waiting time is sampled from a Gamma distribution with alpha=14 ("a" in codes) and beta=1 ("b" in codes) (Reference 3: https://en.wikipedia.org/wiki/Gamma_distribution). This is because I cannot find a proper distribution for waiting time for inter-city movements.
"p" and "gam" in codes are "ρ" and "γ" in Reference 1. "tran_M" is the "ProbabilityMatrix" in Reference 1. "rele" is the "Relevance" values calculated from population data. "distance_m" is the distance matrix between regions. "MaxT" is the number of days.
The unit of time is day.
In addition, when people have only stayed in one area (explored no other areas), they will still return to the current area if they were randomly selected as returners (return to previously visited areas).

The codes finally generate a matrix of shape 1000000x385, where each row indicates a person's movements in 385 days. One entry for one day.
A number indicates a location (number is the index of location in the list "locs").
