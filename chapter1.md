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

* Sõnastada tõestamist vajav *sisukas hüpotees* ($H\_1$) ja selle täiend/vastand *null-hüpotees* ($H\_0$). Tavaliselt vastab null-hüpotees $H\_0$ nn tasakaalu olukorrale ehk sellele, mis on seni kogu aeg kehtinud.
* Valida sobiv *olulisuse nivoo*, ehk vea tegemise tõenäosus $\alpha$. Loomulikult soovime, et see oleks väike. Üldiselt valitakse kas 0.01, 0.05 või 0.1.
* Arvutada *test-statistiku* väärtuse. Test-statistiku valem sõltub hüpoteesist. Praktikumis on jagatud valemilehti, milles saab vajalikud valemid leida.
* Leida sobiva *täiendkvantiili* väärtuse või arvutada test-statistikule vastav olulisuse tõenäosus $p$.
* Tõlgendada saadud tulemused ja teha *otsus* hüpoteeside kohta.

Milline järgnevatest väidetest on tõene?

`@instructions`
- Kui hüpoteesi $H\_1$ tõestada ei õnnestu, siis tõestab see automatselt hüpoteesi $H\_0$.
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
msg1 <- "See on sagedane valetõlgendus. Testid on konstrueeritud nii, et hüpoteesi $H_0$ ei saa kunagi tõestada. Juhul, kui hüpoteesi $H_1$ tõestada ei õnnestu, siis sel juhul me jääme $H_0$ juurde (ehk jääme null seisu juurde). See automaatselt ei tähenda, et $H_0$ on tõene. Võimalik, et meil oli liiga vähe andmeid $H_1$ tõestamiseks."
msg2 <- "Ei ole õige! Kui saame, et $p > \\alpha$, siis järelikult test-statistiku väärtus kriitilisse piirkonda ei sattunud. Selletõttu jääme $H_0$ juurde."
msg3 <- "Ei ole õige! Test-staistiku sattumine kriitilisse piirkonda tõestab hoopis hüpoteesi $H_1$."
msg4 <- "Õige!"

test_mc(correct = 4, feedback_msgs = c(msg1, msg2, msg3, msg4))

# Final message the student will see upon completing the exercise
success_msg("Õige! Test-staistiku sattumine kriitilisse piirkonda näitab seda, et eeldatud null-hüpotees siin kehtida ei saa ja see omakorda tõestab hüpoteesi $H_1$.")
```


---
## Test-statistik

```yaml
type: NormalExercise
key: 7ca0756cea
lang: r
xp: 100
skills: 1
```
After setting the hypotheses, we can use the data we have and calculate a test statistic, which is a statistical summary of the data. What kind of test statistic to use, depends on the situation.

A $z$ test statistic is computed by standardizing a normal random variable (here $\bar{x}$).

$$z = \frac{\bar{x} - \mu_0}{\sigma / \sqrt{n}}$$

where $\mu_0$ is the hypothesized expected value of $\bar{x}$, $\sigma$ is the population standard deviation and $n$ is the sample size. A $z$ test has limited practical use (because it assumes that the population standard deviation is known) but it demonstrates the idea of a test statistic well enough. The widely used t-test is very similar.

Notice that if $\sigma$ is replaced by it's estimate $s$, then the denominator has the standard error of $\bar{x}$.

`@instructions`

`@hint`

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}

```

`@solution`
```{r}

```

`@sct`
```{r}

```
