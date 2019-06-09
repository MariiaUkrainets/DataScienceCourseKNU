Лабораторна робота № 7.
Для виконання роботи можна скористатись бібліотекою stringr від tidyverse
https://stringr.tidyverse.org/index.html

Частина 1.
Завантажте файл “olympics.csv” за посиланням
https://www.dropbox.com/s/9oayr45v7nj30nv/olympics.csv?dl=0
Цей файл базується на статті в Wikipedia All Time Olympic Games Medals Спочатку необхідно провести базову обробку файлу.
Напишіть функцію prepare_set <- function(file_name) {} яка в якості аргументу
приймає ім’я файлу і повертає дата фрейм. Збережіть цей дата фрейм в змінну




```{r}
getwd()
[1] "D:/Documents"

path = "D:/Documents/"
out.file <- ""
file.names <- dir(path, pattern =".csv")
file.names


olympics
olympics <- prepare_set(“olympics.csv”)

library("stringr")
```

Функція prepare_set повинна виконувати наступні дії:

    1. Зчитати файл
```{r}
olympics <- read.csv("olympics.csv", skip = 1, header = TRUE, encoding="UTF-8", stringsAsFactors = FALSE)
```

2. Першому стовпцю дати назву “Country”

3. Автоматично в циклі згенерувати назви останніх стовпців за наступними
правилами:
  3.1. Видалити з назви “X.U.2116..”, тобто “X.U.2116..Summer” буде
“Summer”
3.2. “X01..” замінити на “Gold”, тобто “ X01...1” буде “Gold.1”
3.3. “X02..” та “X03..” замінити на “Silver” та “Bronze” відповідно
В результаті повинні бути наступні назви стовпців: "Country", "Summer",
"Gold", "Silver", "Bronze", "Total", "Winter", "Gold.1", "Silver.1", "Bronze.1",
"Total.1", "Games", "Gold.2", "Silver.2", "Bronze.2", "Combined.total"

4. Необхідно привести назви країн до виду "Afghanistan", "Algeria" і т.п. Для
цього можна використати функцію split. В назві країн не повинно бути
пробілів на початку та в кінці.

5. Додайте до дата фрейму новий стовпець “ID”, в який запишіть трибуквений
код країна. Наприклад, "AFG", "ALG" і т.п.

6. Видаліть з дата фрейму останню строку “Totals”
```{r}
prepare_set <- function(){
    names(olympics)[1] <- 'Country'
    for (i in 1:length(names(olympics))) {
        name <- names(olympics)[i]
        if (str_sub(name, 2,3) == '01' names(olympics)[i] <- str_c('Gold', str_sub(name, 6))
        if (str_sub(name, 2,3) == '02' names(olympics)[i] <- str_c('Silver', str_sub(name, 6))
        if (str_sub(name, 2,3) == '03' names(olympics)[i] <- str_c('Bronze', str_sub(name, 6))
        if (str_sub(name, 3,3) == 'U' names(olympics)[i] <- str_sub(name, 11)
}
    countries <- strsplit(olympics$Country, "(", fixed=TRUE)
    olympics$Country <- sapply(countries, "[", 1)
    olympics$Country <- str_trim(olympics$Country)
    olympics$ID <- sapply(countries, "[", 2)
    olympics$ID <- str_sub(olympics$ID, 1, 3)
    olympics <- olympics[-which(olympics$Country == "Totals"),]
}
tail(olympics$Country)
[1] "Virgin Islands"                  
[2] "Yugoslavia"                      
[3] "Independent Olympic Participants"
[4] "Zambia"                          
[5] "Zimbabwe"                        
[6] "Mixed team" 

```

Для кожного наступного питання напишіть функцію, яка повертає вказаний 
результат. Назви функції “answer_one” для питання 1, “answer_two” для
питання 2 і т.д.
Питання 1
Котра країна виграла найбільшу кількість золотих нагород на літніх іграх?
Функція повинна повернути одне текстове значення.
```{r}
answer_one <- function() {
    olympics[which.max(olympics$Gold), 'Country']
    }

answer_one()
[1] "United States"

```
Питання 2
Яка країна має найбільшу різницю між кількістю нагород на літніх та зимових
іграх?
Функція повинна повернути одне текстове значення.
```{r}
answer_two <- function() {
    olympics[which.max(olympics$Total - olympics$Total.1), 'Country']
    }

answer_two()
[1] "United States"


```
Питання 3
В якій крайні найбільша різниця між літніми та зимовими золотими нагородами
відносно до загальної кількості нагород (Summer Gold - Winter Gold) / Total Gold.
Врахувати тільки країни які мають як мінімум по одній нагороді в літніх та
зимових іграх.
Функція повинна повернути одне текстове значення.
```{r}
answer_three <- function() {
    olympics[which.max((olympics$Gold - olympics$Gold.1)/(olympics$Gold + olympics$Gold.1)), 'Country']
    }

answer_three()
```
Питання 4
Необхідно знайти кількість балів по кожній крайні. Бали рахуються наступним
чином: Золота нагорода Gold.2 це три бали, срібна Silver.2 - 2 бали та бронзова
Bronze.2 – 1 бал.
Функція повинна повертати дата фрейм довжиною 146, який складається з двох
колонок: "Country", "Points".
```{r}

```

Частина 2.
Для наступних питань використаємо дані перепису населення від United States
Census Bureau. Цей набір даних містить дані по населенню для округів і штатів в
США з 2010 по 2015 рокі. В цьому документі є опис назв змінних.
Завантажити файл можна за посиланням
https://www.dropbox.com/s/c1b2vqg8i3m1n93/census.csv?dl=0
Файл необхідно завантажити в змінну census_df
#Зчитуємо файл
census_df <- read.csv("census.csv", stringsAsFactors = FALSE)
Питання 5
В якому штаті (state) більше всього округів (county)?
Функція повинна повернути одне текстове значення
Питання 6
Якщо розглядати три найбільш населених округа (county) з кожного штату, які три
найбільш населені штати (в порядку з більш до менш населеного)?
Використовуйте CENSUS2010POP.
Функція повинна повернути вектор з трьох текстових значень.
Питання 7
Який округ (county) має найбільшу абсолютну зміну в населенні протягом
періоду 2010-2015?
(Підказка: значення населення зберігається в колонках з POPESTIMATE2010 до
         POPESTIMATE2015. Необхідно розглядати всі шість колонок).
Якщо населення округу за 5річний період 100, 120, 80, 105, 100, 130, то найбільша
різниця за період буде |130-80|=50.
Функція повинна повернути одне текстове значення.
Питання 8
В census_df США поділені на 4 регіони (колонка "REGION"). Напишіть функцію,
яка знаходить округи (county), що належать регіонам 1 або 2, назва яких
починається з "Washington" та POPESTIMATE2015 більше ніж POPESTIMATE2014.
Функція повинна повернути 5х2 дата фрейм з колонками "STNAME", "CTYNAME".
