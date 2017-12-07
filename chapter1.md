---
title       : Hüpoteeside kontroll ning seose modelleerimine regressiooni abil
description : Selles viimases praktikumis õpime funktsioone hüpoteeside kontrollimiseks T testi abil. Seejärel tutvume võimalustega seose hindamiseks kahe tunnuse vahel ning selle modelleerimiseks regressiooni abil. 

---
## Statistilise hüpoteesi kontroll

```yaml
type: MultipleChoiceExercise
lang: r
xp: 100
skills: 1
key: 7ba74f43f0
```

Tere tulemast viimasele praktikumile! Alustame statistiliste hüpoteeside sõnastamise ja kontrollimisega. Sõnastame hüpoteetilise väite ($H_1$) parameetri kohta ja soovime seda väidet tõestada valimiandmete põhjal. Üldiselt tuleks selle jaoks teostada järgmisi samme:

* Sõnastada tõestamist vajav hüpotees ($H1$) ja selle täiend/vastand hüpotees ($H_0$). Tavaliselt vastab null-hüpotees $H_0$ nn tasakaalu olukorrale ehk sellele, mis on seni kogu aeg kehtinud.
* Valida sobiv olulisuse nivoo, ehk vea tegemise tõenäosus $\alpha$. Loomulikult soovime, et see oleks väike. Üldiselt valitakse kas 0.01, 0.05 või 0.1.
* Arvutada test-statistiku väärtus. Test-statistiku valem sõltub hüpoteesist. Praktikumis on jagatud valemilehti, milles saab leida vajalikud valemid.
* Leida sobiva täiend-kvantiili väärtus või arvutada test-statistikule vastav olulisuse tõenäosus $p$.
* Tõlgendada saadud tulemused ja teha otsus hüpoteeside kohta.

Milline väide on tõene?

`@instructions`
- Adventure
- Action
- Animation
- Comedy

`@hint`
Have a look at the plot. Which color does the point with the lowest rating have?

`@pre_exercise_code`
```{r}
# The pre exercise code runs code to initialize the user's workspace.
# You can use it to load packages, initialize datasets and draw a plot in the viewer

movies <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/course/introduction_to_r/movies.csv")

library(ggplot2)

ggplot(movies, aes(x = runtime, y = rating, col = genre)) + geom_point()
```

`@sct`
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

msg_bad <- "That is not correct!"
msg_success <- "Exactly! There seems to be a very bad action movie in the dataset."
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_success, msg_bad, msg_bad))
```

---
## More movies

```yaml
type: NormalExercise
lang: r
xp: 100
skills: 1
key: 8a76a5a3d2
```

In the previous exercise, you saw a dataset about movies. In this exercise, we'll have a look at yet another dataset about movies!

A dataset with a selection of movies, `movie_selection`, is available in the workspace.

`@instructions`
- Check out the structure of `movie_selection`.
- Select movies with a rating of 5 or higher. Assign the result to `good_movies`.
- Use `plot()` to  plot `good_movies$Run` on the x-axis, `good_movies$Rating` on the y-axis and set `col` to `good_movies$Genre`.

`@hint`
- Use `str()` for the first instruction.
- For the second instruction, you should use `...[movie_selection$Rating >= 5, ]`.
- For the plot, use `plot(x = ..., y = ..., col = ...)`.

`@pre_exercise_code`
```{r}
# You can also prepare your dataset in a specific way in the pre exercise code
load(url("https://s3.amazonaws.com/assets.datacamp.com/course/teach/movies.RData"))
movie_selection <- Movies[Movies$Genre %in% c("action", "animated", "comedy"), c("Genre", "Rating", "Run")]

# Clean up the environment
rm(Movies)
```

`@sample_code`
```{r}
# movie_selection is available in your workspace

# Check out the structure of movie_selection


# Select movies that have a rating of 5 or higher: good_movies


# Plot Run (i.e. run time) on the x axis, Rating on the y axis, and set the color using Genre

```

`@solution`
```{r}
# movie_selection is available in your workspace

# Check out the structure of movie_selection
str(movie_selection)

# Select movies that have a rating of 5 or higher: good_movies
good_movies <- movie_selection[movie_selection$Rating >= 5, ]

# Plot Run (i.e. run time) on the x axis, Rating on the y axis, and set the color using Genre
plot(good_movies$Run, good_movies$Rating, col = good_movies$Genre)
```

`@sct`
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

test_function("str", args = "object",
              not_called_msg = "You didn't call `str()`!",
              incorrect_msg = "You didn't call `str(object = ...)` with the correct argument, `object`.")

test_object("good_movies")

test_function("plot", args = "x")
test_function("plot", args = "y")
test_function("plot", args = "col")

test_error()

success_msg("Good work!")
```
