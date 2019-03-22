Ћабораторна робота є 3

¬ лабораторн≥й робот≥ необх≥дно написати наступн≥ функц≥њ на мов≥ R та вивести
результат роботи цих функц≥й на дов≥льних даних:
1. ‘ункц≥€ add2(x, y), €ка повертаЇ суму двох чисел
```{r}
add2 <- function(x,y) {x+y}
add2(5,5)
[1] 10

```
2. ‘ункц≥€ above(x, n), €ка приймаЇ вектор та число n, та повертаЇ вс≥ елемент≥ вектору, €к≥ б≥льше n. ѕо замовчуванню n = 10.

```{r}
above <- function(x, n=10) {
  logic <- logical(length(x))
  for (i in 1:length(x)) {
    if (x[i] > n) {logic[i] <- TRUE}
    else {logic[i] <- FALSE}
  }
  x[logic]
} 
x <- c(4, 5, 6, 7, 12, 55, 44)
above(x, n)
[1] 12 55 44

above1 <- function(x, n=10) {
  x[x>n]
}
[1] 12 55 44

```

3. ‘ункц≥€ my_ifelse(x, exp, n), €ка приймаЇ вектор x, пор≥внюЇ вс≥ його елементи за допомогою exp з n, та повертаЇ елементи вектору, €к≥ в≥дпов≥дають умов≥ expression. 
Ќаприклад, my_ifelse(x, У>Ф, 0) повертаЇ вс≥
елементи x, €к≥ б≥льш≥ 0. Exp може дор≥внювати У<Ф, У>Ф, У<=Ф, У>=Ф, У==Ф. якщо exp не сп≥впадаЇ н≥ з одним з цих вираз≥в, повертаЇтьс€ вектор x.

```{r}
my_ifelse <- function(x, exp, n) {
  if (exp == '==') {res=x[x==n]}
  else if (exp == '<') {res=x[x<n]}
  else if (exp == '>') {res=x[x>n]}
  else if (exp == '<=') {res=x[x<=n]}
  else if (exp == '>=') {res=x[x>=n]}
  else {res=x}
   res
}

x <- c(4, -5, 6, 7, -12, 55, 44)
my_ifelse(x, '>', 0)
[1]  4  6  7 55 44

```

4. ‘ункц≥€ columnmean(x, removeNA), €ка розраховуЇ середнЇ значенн€(mean) по кожному стовпцю матриц≥, або data frame. Ћог≥чний параметр removeNA вказуЇ, чи видал€ти NA значенн€. ѕо замовчуванню в≥н дор≥внюЇ TRUE.
```{r}
x <- data.frame('A'=c(1, 5, 6, 5, 9, NA), 'B'=c(NA, 5, 6,     5, 9, 15), 'C'=c(NA, 5, NA, 17, 9, 15))
x

   A  B  C
1  1 NA NA
2  5  5  5
3  6  6 NA
4  5  5 17
5  9  9  9
6 NA 15 15

columnmean <- function(x, removeNA=TRUE) {
  n <- ncol(x)
  v <- numeric(n)
  for (i in 1:n) {
    v[i] <- mean(x[,i], na.rm=removeNA)
  }
  v
}

columnmean(x)
[1]  5.2  8.0 11.5

```
