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
Kui huvipakkuv sisukas hüpotees on sõnastatud, saame kasutada valimiandmeid, et väljaarvutada test-statistiku väärtuse. Millist test-statistikut kasutada, sõltub situatsioonist. Vaatame siin **suure valimi olukorda** (valimimaht on vähemalt 60), siis saame kasutada test-statistikut $Z$, mille jaotus on ligikaudu $N(0,\ 1)$ (põhjalikum ülevaade on antud loengul):

$$Z = \frac{\bar{x} - \mu_0}{s / \sqrt{n}}.$$

Siin on $\bar{x}$ valimiandmete keskmine, $s$ on valimi standardhälve ja $\mu_0$ on konstant, millega soovitakse üldkogumi keskväärtust võrrelda sisuka hüpoteesi väites.

`@instructions`

1. Muutuja `kt2` on juba loodud. See sisaldab 2. kontrolltöö tulemusi ühel eelneval aastal. Uuri neid. Omista muutujale `n` valimimahu (ehk vektori `kt2` elementide arvu).
2. Null-hõpotees väidab, et kontrolltöö keskmine on 14 punkti: $H_0: \ \mu=14$. Omista muutujale $mu0$ väärtuse 14.
3. Arvuta valimikeskmine ja standardhälve (muutujad vastavalt `x_kesk` ja `s`).
4. Leia test-statistiku `Z` väärtus ülalpool toodud valemi abil. Millega võrdub?
5. Käivita käsk `zplot(Z)`, et visualiseerida muutujale `Z` vastav jaotus `N(0, 1)` ja muutuja `Z` asukoht sellel graafikul.

According to the picture and assuming that $Z \sim N(0,1)$, what is the probability that the test statistic $Z$ would take on a value even further away from it's expected value than the current value $z$? Save this probability to the object p.

`@hint`

`@pre_exercise_code`
```{r}
kt2 <- c(19.7, 19.2, 16.6, 16.5, 8.7, 7.9, 10.4, 18.5, 17.1, 19.3, 12.8, 13.0, 12.4, 18.5, 9.7, 12.6, 12.9, 18.6, 20.0, 16.8, 17.1, 7.2, 8.6, 10.1,
         18.0, 17.8, 19.6, 13.1, 13.1, 14.6, 18.8, 9.8, 13.6, 12.9, 19.2, 19.7, 15.9, 16.8, 9.2, 5.4, 10.1, 17.7, 17.0, 19.9, 12.3, 13.1, 11.1, 19.3,
         9.3, 13.4, 13.1, 19.0, 19.7, 16.5, 16.1, 8.1, 7.4, 9.5, 18.7, 17.3, 19.6, 12.6, 11.7, 13.8, 19.3, 10.3, 14.1, 13.1)


zplot <- function(critical) {
  critical <- round(critical, 2)
  z <- c(-critical, critical)
  par(mar = c(7,4,5,4))
  x <- (-40:40)/10
  y <- dnorm(x)
  main = paste("The N(0, 1) distribution \n z = ",critical)
  plot(x, y, type = "l", xaxt = "n", ylab = "n", main = main)
  axis(1, at = c(-3,  0,  3))
  axis(1, at = round(z, 2) , col.ticks = "red", las = 2)
  
  # highlight critical regions, add matching percentages
  x1 <- x[x<=min(z)]; x2 <- x[x>=max(z)]
  a <- round(pnorm(min(z)),2)
  
polygon(c(min(x1),x1, max(x1), min(x2), x2, max(x2)),
            c(0, dnorm(x1),0, 0, dnorm(x2), 0), col = "grey60")
      text(x = c(-3.5, 3.5), y = c(0.08,0.08), labels = paste0(a*100,"%"), cex = 1.5)
      text(x = 0, y = 0.08, labels=paste0(100*(1-a*2),"%"), cex = 1.5)
}
```

`@sample_code`
```{r}
# learning2014 is available

# Strategic learning scores and number of observations
stra <- learning2014$stra
n <- length(stra)

# H0: mu = 3
mu0 <- 3

# Sample mean of strategic learning
x_bar <- 

# Standard error of the sample mean
error <-

# The test statistic
z <- (x_bar - mu0) / error

# Print out the value of the test statistic


# Visualize the N(0, 1) distribution and the value of z 
zplot(z)

# P(|Z| > z)
p <- 

```

`@solution`
```{r}

```

`@sct`
```{r}

```
