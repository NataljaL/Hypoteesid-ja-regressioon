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

* Sõnastada tõestamist vajav hüpotees ($H\_1$) ja selle täiend/vastand hüpotees ($H\_0$). Tavaliselt vastab null-hüpotees $H\_0$ nn tasakaalu olukorrale ehk sellele, mis on seni kogu aeg kehtinud.
* Valida sobiv olulisuse nivoo, ehk vea tegemise tõenäosus $\alpha$. Loomulikult soovime, et see oleks väike. Üldiselt valitakse kas 0.01, 0.05 või 0.1.
* Arvutada test-statistiku väärtuse. Test-statistiku valem sõltub hüpoteesist. Praktikumis on jagatud valemilehti, milles saab vajalikud valemid leida.
* Leida sobiva täiend-kvantiili väärtuse või arvutada test-statistikule vastav olulisuse tõenäosus $p$.
* Tõlgendada saadud tulemused ja teha otsus hüpoteeside kohta.

Milline järgnevatest väidetest on tõene?

`@instructions`
- Kui hüpoteesi $H\_1$ ei õnnestu tõestada, siis tõestab see automatselt hüpoteesi $H\_0$.
- Kui saame, et $p>\alpha$, siis tõestab see hüpoteesi $H\_1$.
- Kui test-statistiku $T$ väärtus langeb kriitilisse piirkonda, mis on määratud täiendkvantiili abil, siis tõestab see hüpoteesi $H_0$.
- Kui test-statistiku $T$ väärtus langeb kriitilisse piirkonda, mis on määratud täiendkvantiili abil, siis tõestab see hüpoteesi $H_1$.

`@hint`
Lihtsalt proovi erinevaid variante läbi ja saad vastava tagasiside.

`@pre_exercise_code`
```{r}
# puudub
```

`@sct`
```{r}
msg1 <- "See on sagedane valetõlgendus. Testid on konstrueeritud nii, et hüpoteesi $H_0$ ei saa kunagi tõestada. Juhul, kui ei hüpoteesi $H_1$ tõestada ei õnnestu, siis sel juhul me jääme $H_0$ juurde (ehk jääme null seisu juurde). See automaatselt ei tähenda et $H_0$ on tõene. Võimalik, et meil oli liiga vähe andmeid $H_1$ tõestamiseks."
msg2 <- "Kui saame, et $p>\alpha$, siis järelikult test-statistiku väärtus kriitilisse piirkonda ei sattunud. Selletõttu jääme $H_0$ juurde."
msg3 <- "Test-staistiku sattumine kriitilisse piirkonda tõestab hüpoteesi $H_1$."
msg4 <- "Õige! Test-staistiku sattumine kriitilisse piirkonda näitab seda, et eeldatud null-hüpotees siin kehtida ei saa ja see omakorda tõestab hüpoteesi $H_1$."

test_mc(correct = 4, feedback_msgs = c(msg1, msg2, msg3, msg4))

# Final message the student will see upon completing the exercise
success_msg("Tubli töö!")
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
