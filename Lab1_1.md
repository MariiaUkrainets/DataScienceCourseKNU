Лабораторна робота № 1 

В лабораторній роботі необхідно виконати наступні дії:

1. Створити змінні базових (atomic) типів. Базові типи: character, numeric,
integer, complex, logical.

```{r}
> charac <- "program"
> print(charac)
[1] "program"
> 
> numer <- 678.678
> print(numer)
[1] 678.678
> 
> integ <- 4769L 
> print(integ)
[1] 4769
> 
> compl <- 56+6i
> print(compl)
[1] 56+6i

> logic <- FALSE
> logic
[1] FALSE

```
2. Створити вектори, які: містить послідовність з 5 до 75; містить числа 3.14, 2.71, 0, 13; 100 значень TRUE.

```{r}
> vect_1 <- c(5:75)
> vect_1
 [1]  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24
[21] 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44
[41] 45 46 47 48 49 50 51 52 53 54 55 56 57 58 59 60 61 62 63 64
[61] 65 66 67 68 69 70 71 72 73 74 75

> vect_2 <- c(3.14, 2.71, 0, 13)
> vect_2
[1]  3.14  2.71  0.00 13.00

> rep(T, 100)
  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
 [13] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
 [25] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
 [37] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
 [49] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
 [61] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
 [73] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
 [85] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
 [97] TRUE TRUE TRUE TRUE

```

3. Створити наступну матрицю за допомогою matrix, та за допомогою cbind
або rbind
0.5 1.3 3.5
3.9 131 2.8
0 2.2 4.6
2 7 5.1

```{r}
> matr <- matrix(c(0.5, 3.9, 0, 2, 1.3, 131, 2.2, 7, 3.5, 2.8, 4.6, 5.1), nrow = 4, ncol = 3)
> matr
     [,1]  [,2] [,3]
[1,]  0.5   1.3  3.5
[2,]  3.9 131.0  2.8
[3,]  0.0   2.2  4.6
[4,]  2.0   7.0  5.1

> c1 <- c(0.5, 3.9, 0, 2)
> c2 <- c(1.3, 131, 2.2, 7)
> c3 <- c(3.5, 2.8, 4.6, 5.1)
> cbind(c1, c2, c3)
      c1    c2  c3
[1,] 0.5   1.3 3.5
[2,] 3.9 131.0 2.8
[3,] 0.0   2.2 4.6
[4,] 2.0   7.0 5.1

```

4. Створити довільний список (list), в який включити всі базові типи.
```{r}
> list_1 <- list(charac, numer, integ, compl, logic)
> list_1
[[1]]
[1] "program"

[[2]]
[1] 678.678

[[3]]
[1] 4769

[[4]]
[1] 56+6i

[[5]]
[1] FALSE

```

5. Створити фактор з трьома рівнями «baby», «child», «adult».
```{r}
> fact <- c(1, 1, 2, 2, 3, 1, 2)
> fact <- factor(fact, levels=c(1,2,3))
> levels(fact) <- c("baby", "child", "adult")
> fact
[1] baby  baby  child child adult baby  child
Levels: baby child adult

```

6. Знайти індекс першого значення NA в векторі 1, 2, 3, 4, NA, 6, 7, NA, 9, NA, 11. Знайти кількість значень NA.
```{r}
> vectNA <- c(1, 2, 3, 4, NA, 6, 7, NA, 9, NA, 11)
> match(NA, vectNA)
[1] 5
> sum(is.na(vectNA))
[1] 3


```

7. Створити довільний data frame та вивести в консоль.
```{r}
> city <- c("New York", "Chicago", "New York", "Chicago", "Houston", "Houston")
> sex <- c("Male", "Female", "Male", "Female", "Male", "Female")
> salary <- c(24000, 21500, 23800, 26400, 25900, 24600)
> CITY <- data.frame(City = city, Sex = sex, Salary = salary)
> CITY
      City    Sex Salary
1 New York   Male  24000
2  Chicago Female  21500
3 New York   Male  23800
4  Chicago Female  26400
5  Houston   Male  25900
6  Houston Female  24600

```

8. Змінити імена стовпців цього data frame.
```{r}
> colnames(CITY) <- c("CITY", "SEX", "SALARY")
> CITY
      CITY    SEX SALARY
1 New York   Male  24000
2  Chicago Female  21500
3 New York   Male  23800
4  Chicago Female  26400
5  Houston   Male  25900
6  Houston Female  24600

```




