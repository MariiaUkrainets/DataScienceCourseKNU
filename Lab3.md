����������� ������ � 3

� ����������� ����� ��������� �������� ������� ������� �� ��� R �� �������
��������� ������ ��� ������� �� �������� �����:
1. ������� add2(x, y), ��� ������� ���� ���� �����
```{r}
add2 <- function(x,y) {x+y}
add2(5,5)
[1] 10

```
2. ������� above(x, n), ��� ������ ������ �� ����� n, �� ������� �� ������� �������, �� ����� n. �� ������������ n = 10.

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

3. ������� my_ifelse(x, exp, n), ��� ������ ������ x, ������� �� ���� �������� �� ��������� exp � n, �� ������� �������� �������, �� ���������� ���� expression. 
���������, my_ifelse(x, �>�, 0) ������� ��
�������� x, �� ����� 0. Exp ���� ���������� �<�, �>�, �<=�, �>=�, �==�. ���� exp �� ������� � � ����� � ��� ������, ����������� ������ x.

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

4. ������� columnmean(x, removeNA), ��� ��������� ������ ��������(mean) �� ������� ������� �������, ��� data frame. ������� �������� removeNA �����, �� �������� NA ��������. �� ������������ �� ������� TRUE.
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
