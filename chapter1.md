---
title       : Hüpoteeside kontroll
description : Selles osas õpime võimalusi hüpoteeside kontrollimiseks.

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
2. Null-hõpotees väidab, et kontrolltöö keskmine on 15.5 punkti: $H_0: \ \mu=15.5$. Sisukas hüpotees aga $H\_1: \mu\neq 15.5$. Omista muutujale `mu0` väärtuse 15.5.
3. Arvuta valimikeskmine ja standardhälve (muutujad vastavalt `x_kesk` ja `s`).
4. Leia test-statistiku `Z` väärtus ülalpool toodud valemi abil. Millega võrdub?
5. Käivita käsk `zplot(Z)`, et visualiseerida muutujale `Z` vastav jaotus `N(0, 1)` ja muutuja `Z` asukoht sellel graafikul.
6. Millega võrdub diagrammi järgi test-statistikule vastav olulisuse tõenäosus $p$? Tuleta meelde, et kahepoolse hüpoteesi kontrollimisel on $p=P(|Z| > z)$, kus $z$ valimi põhjal arvutatud test-statistiku $Z$ väärtus. Omista leitud tõenäosus muutujale `p`.

Otsus hüpoteeside kohta on järgmine: kui $p < \alpha$, siis hüpotees $H_1$ on tõestatud. Kui võtta $\alpha=0.05$, siis millise otsuse saame?

`@hint`
* Olulisuse tõenäosuse $p$ leidmiseks tuleks vaadata diagrammil sabades olevaid pindalaid (nii vasakul kui ka paremal). Millega võrdub kogu sabades olev pindala?
* Tähtis on meeles pidada, et $p$ on tõenäosus, järelikult on selle väärtuste piirkond on 0-st 1-ni.
* $|Z|$ on juhusliku suuruse $Z$ absoluutväärtus, st et $P(|Z| > z) = P(Z < -z) + P(Z > z)$.

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
# 1. Vaata muutja kt2 väärtuseid ja leia valimimaht:
kt2
n <- 

# 2. H0: mu = 15.5. Omista mu0 väärtus:
mu0 <- 

# 3. Leia valimikeskmine ja standardhölve:
x_kesk <- 
s <- 

# 4. Leia test-statistiku väärtus ja väljasta:
Z <- 
Z

# 5. Käivita käsk ja uuri saadud disagrammi:
zplot(Z)

# 6. Millega võrdub p=P(|Z| > z)? Vastus on leitav diagrammil!
p <- 

```

`@solution`
```{r}
# 1. Vaata muutja kt2 väärtuseid ja leia valimimaht:
kt2
n <- length(kt2)

# 2. H0: mu = 15.5. Omista mu0 väärtus:
mu0 <- 15.5

# 3. Leia valimikeskmine ja standardhölve:
x_kesk <- mean(kt2)
s <- sd(kt2)

# 4. Leia test-statistiku väärtus ja väljasta:
Z <- (x_kesk - mu0) / (s/sqrt(n))
Z

# 5. Käivita käsk ja uuri saadud disagrammi:
zplot(Z)

# 6. Millega võrdub p=P(|Z| > z)? Vastus on leitav diagrammil!
p <- 0.04

```

`@sct`
```{r}
# submission correctness tests

test_object("n", undefined_msg = "Loo muutuja `n`, mis vastab valimimahule.",
            incorrect_msg = "Väärtus on vale. Kas kasutasid funktsioon `length()`?")
test_object("x_kesk", undefined_msg = "Loo muutuja `x_kesk`, mis vastab valimi keskmisele.",
            incorrect_msg = "Väärtus on vale. Kas kasutasid funktsioon `mean()`?")
test_object("s", undefined_msg = "Loo muutuja `s`, mis vastab valimi standardhälbele.",
            incorrect_msg = "Väärtus on vale. Kas kasutasid funktsioon `sd()`?")
test_object("Z", undefined_msg = "Loo muutuja `Z`, mis vastab test-statistikule.",
            incorrect_msg = "Väärtus on vale. Vaata valemit selgituses.")
test_object("p", undefined_msg = "Loo muutuja `p`, mis vastab olulisuse tõenäosusele. Selle väärtus on leitav diagrammil",
            incorrect_msg = "Väärtus on vale. Proovi uuesti.")

test_error()

# Final message the student will see upon completing the exercise
success_msg("Suurepärane töö! Kui võtta vea tegemise tõenäosuseks 0.05, siis saadud $p=0.04$ väärtuse korral langeb test-statistik kriitilisse piirkonda ja hüpotees $H_1: \ \mu\neq 15.5$ on tõestatud!")
```
