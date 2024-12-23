---
layout: page
title:  Pave the World
tags: geospatial terra R GHGs
summary: Calculating the greenhouse gas emissions from paving over soil with concrete.
image: ../assets/pave_the_world/co2e_ghg_comparison.jpg
width: 100%
caption: Soil emissions of carbon dioxide, methane and nitrous oxide from sealing.
highlight: true
---

This project was a dissertation for my Master's degree in Data Science. It was very challenging but I learnt a lot about working with spatial data. I especially enjoyed the occasions when I reached out to my supervisors and the authors of some papers I was reading. When completing projects in the future I will make an effort to do more of that as I think it makes them both more enjoyable and better.

### Main results
We determined that paving over soil with concrete very likely reduces GHG emissions from the *soil* specifically. *Soil* being the key word here because our analysis does not consider the additional ecosystem services of soil. For instance:

- How did that forest that was on the car park before it was built affect GHG emissions? 
- How has the flood risk changed now there is concrete preventing water from being soaked up by soil?
- How has the temperature in the area changed since the city was built due to the albedo effect?
- And the list goes on. 

So whilst we did find out a lot about the change in soil GHG emissions from paving over soil, the story is not over yet.

### Reflecting
I used the R packages `terra`, `ggplot2` and the in-process database management system [DuckDB][duck-db] to carry out the analysis. DuckDB was a relatively late addition to the project but was really great. Next time, I would have researched alternate methods to R like the extension to [PostgreSQL][PostgreSQL], [PostGIS][PostGIS], as I believe a system like that would have made running  the pipeline significantly quicker - particularly if combined with some kind of cloud computing system. 

On a non-technical note, next time I do a large project I am going to spend more time dedicated to thinking about parts of the problem with a pen and paper as this seemed to be when my work was at it's best. With recent personal projects this has made all the difference - and made them more enjoyable too. I have always particularly enjoyed working on problems with a pen and paper.

### See the full project:

- The dissertation can be found here: [get pdf]({{site.url}}/assets/pave_the_world/Freddy_Dissertation.pdf)
- And a poster submitted for the project: [get pdf]({{site.url}}/assets/poster.pdf) 

[duck-db]: https://duckdb.org/
[PostgreSQL]: https://www.postgresql.org/
[PostGIS]: https://postgis.net/
