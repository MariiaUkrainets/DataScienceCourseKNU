Лабораторна робота № 3 

В лабораторній роботі необхідно написати наступні функції на мові R та вивести
результат роботи цих функцій на довільних даних:
1. Функція add2(x, y), яка повертає суму двох чисел.
```{r}
add2 <- function(x,y) {x+y}
add2(5,5)
[1] 10

```
2. Функція above(x, n), яка приймає вектор та число n, та повертає всі елементі вектору, які більше n. По замовчуванню n = 10.

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

3. Функція my_ifelse(x, exp, n), яка приймає вектор x, порівнює всі його
елементи за допомогою exp з n, та повертає елементи вектору, які
відповідають умові expression. Наприклад, my_ifelse(x, “>”, 0) повертає всі
елементи x, які більші 0. Exp може дорівнювати “<”, “>”, “<=”, “>=”, “==”.
Якщо exp не співпадає ні з одним з цих виразів, повертається вектор x.

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

4. Функція columnmean(x, removeNA), яка розраховує середнє значення
(mean) по кожному стовпцю матриці, або data frame. Логічний параметр
removeNA вказує, чи видаляти NA значення. По замовчуванню він
дорівнює TRUE.
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
