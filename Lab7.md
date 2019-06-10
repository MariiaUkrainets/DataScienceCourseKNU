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

library("stringr")
```

Функція prepare_set повинна виконувати наступні дії:

1. Зчитати файл

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
prepare_set <- function(file_name){
    olympics <- read.csv(file_name, skip = 1, header = TRUE, encoding="UTF-8", stringsAsFactors = FALSE)
    names(olympics)[1] <- 'Country'
    for (i in 1:length(names(olympics))) {
        name <- names(olympics)[i]
        if (str_sub(name, 2,3) == '01') names(olympics)[i] <- str_c('Gold', str_sub(name, 6))
        if (str_sub(name, 2,3) == '02') names(olympics)[i] <- str_c('Silver', str_sub(name, 6))
        if (str_sub(name, 2,3) == '03') names(olympics)[i] <- str_c('Bronze', str_sub(name, 6))
        if (str_sub(name, 3,3) == 'U') names(olympics)[i] <- str_sub(name, 11)
}
    countries <- strsplit(olympics$Country, "(", fixed=TRUE)
    olympics$Country <- sapply(countries, "[", 1)
    olympics$Country <- str_trim(olympics$Country)
    olympics$ID <- sapply(countries, "[", 2)
    olympics$ID <- str_sub(olympics$ID, 1, 3)
    olympics <- olympics[-which(olympics$Country == "Totals"),]
    olympics
}
olympics <- prepare_set('olympics.csv')

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
    olympics <- subset(olympics, Gold>0 & Gold.1>0)
    olympics[which.max((olympics$Gold - olympics$Gold.1)/(olympics$Gold + olympics$Gold.1)), 'Country']
    }

answer_three()
[1] "Bulgaria"

```
Питання 4
Необхідно знайти кількість балів по кожній крайні. Бали рахуються наступним
чином: Золота нагорода Gold.2 це три бали, срібна Silver.2 - 2 бали та бронзова
Bronze.2 – 1 бал.
Функція повинна повертати дата фрейм довжиною 146, який складається з двох
колонок: "Country", "Points".
```{r}
answer_four <- function() {
    Points <- olympics$Gold.2*3 + olympics$Silver.2*2 + olympics$Bronze.2*2
    df <- data.frame(olympics$Country, Points)
    names(df) <- c('Country', 'Points')
    df
    }

answer_four()

                             Country Points
1                        Afghanistan      4
2                            Algeria     35
3                          Argentina    158
4                            Armenia     25
5                        Australasia     27
6                          Australia   1104
7                            Austria    685
8                         Azerbaijan     58
9                            Bahamas     29
10                           Bahrain      2
11                          Barbados      2
12                           Belarus    198
13                           Belgium    332
14                           Bermuda      2
15                           Bohemia      8
16                          Botswana      2
17                            Brazil    239
18               British West Indies      4
19                          Bulgaria    492
20                           Burundi      3
21                          Cameroon     13
22                            Canada   1019
23                             Chile     28
24                             China   1265
25                          Colombia     40
26                        Costa Rica      9
27                       Ivory Coast      2
28                           Croatia     78
29                              Cuba    490
30                            Cyprus      2
31                    Czech Republic    157
32                    Czechoslovakia    387
33                           Denmark    403
34                          Djibouti      2
35                Dominican Republic     15
36                           Ecuador      5
37                             Egypt     59
38                           Eritrea      2
39                           Estonia     93
40                          Ethiopia    111
41                           Finland   1069
42                            France   1793
43                             Gabon      2
44                           Georgia     56
45                           Germany   1816
46            United Team of Germany    310
47                      East Germany   1230
48                      West Germany    553
49                             Ghana      8
50                     Great Britain   1858
51                            Greece    252
52                           Grenada      3
53                         Guatemala      2
54                            Guyana      2
55                             Haiti      4
56                         Hong Kong      7
57                           Hungary   1131
58                           Iceland      8
59                             India     61
60                         Indonesia     60
61                              Iran    135
62                              Iraq      2
63                           Ireland     67
64                            Israel     15
65                             Italy   1561
66                           Jamaica    151
67                             Japan   1026
68                        Kazakhstan    135
69                             Kenya    197
70                       North Korea    112
71                       South Korea    699
72                            Kuwait      4
73                        Kyrgyzstan      6
74                            Latvia     55
75                           Lebanon      8
76                     Liechtenstein     20
77                         Lithuania     48
78                        Luxembourg      9
79                         Macedonia      2
80                          Malaysia     12
81                         Mauritius      2
82                            Mexico    137
83                           Moldova     14
84                          Mongolia     50
85                        Montenegro      2
86                           Morocco     50
87                        Mozambique      5
88                           Namibia      8
89                       Netherlands    866
90              Netherlands Antilles      2
91                       New Zealand    242
92                             Niger      2
93                           Nigeria     49
94                            Norway   1128
95                          Pakistan     23
96                            Panama      7
97                          Paraguay      2
98                              Peru      9
99                       Philippines     18
100                           Poland    652
101                         Portugal     50
102                      Puerto Rico     16
103                            Qatar      8
104                          Romania    692
105                           Russia   1219
106                   Russian Empire     17
107                     Soviet Union   2881
108                     Unified Team    324
109                     Saudi Arabia      6
110                          Senegal      2
111                           Serbia     15
112            Serbia and Montenegro     20
113                        Singapore      8
114                         Slovakia     67
115                         Slovenia     74
116                     South Africa    175
117                            Spain    304
118                        Sri Lanka      4
119                            Sudan      2
120                         Suriname      5
121                           Sweden   1447
122                      Switzerland    743
123                            Syria      7
124                   Chinese Taipei     44
125                       Tajikistan      6
126                         Tanzania      4
127                         Thailand     55
128                             Togo      2
129                            Tonga      2
130              Trinidad and Tobago     38
131                          Tunisia     23
132                           Turkey    215
133                           Uganda     16
134                          Ukraine    279
135             United Arab Emirates      3
136                    United States   6434
137                          Uruguay     22
138                       Uzbekistan     48
139                        Venezuela     26
140                          Vietnam      4
141                   Virgin Islands      2
142                       Yugoslavia    200
143 Independent Olympic Participants      6
144                           Zambia      4
145                         Zimbabwe     19
146                       Mixed team     42
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
```{r}
census_df <- read.csv("census.csv", stringsAsFactors = FALSE)
head(census_df)

answer_five <- function() {
    state <- split(census_df, census_df$STNAME)
    city <- sapply(state, nrow)
    names(which.max(city))
    }

answer_five()
[1] "Texas"
```
Питання 6
Якщо розглядати три найбільш населених округа (county) з кожного штату, які три
найбільш населені штати (в порядку з більш до менш населеного)?
Використовуйте CENSUS2010POP.
Функція повинна повернути вектор з трьох текстових значень.
```{r}
answer_six <- function() {
    census_order <- census_df[order(census_df$STNAME, -census_df$CENSUS2010POP), ]
    stname <- split(census_order, census_order$STNAME)
    stname <- lapply(stname, function(x) sum(x[2:4, 'CENSUS2010POP']))
    stname <- stname[order(unlist(stname), decreasing = TRUE, na.last=TRUE)]
    names(stname)[1:3]
    }

answer_six()
[1] "California" "Texas"      "Illinois"

```
Питання 7
Який округ (county) має найбільшу абсолютну зміну в населенні протягом
періоду 2010-2015?
(Підказка: значення населення зберігається в колонках з POPESTIMATE2010 до
         POPESTIMATE2015. Необхідно розглядати всі шість колонок).
Якщо населення округу за 5річний період 100, 120, 80, 105, 100, 130, то найбільша
різниця за період буде |130-80|=50.
Функція повинна повернути одне текстове значення.
```{r}
answer_seven <- function() {
  df2 <- census_df[,10:15]
  df2$MAX <- apply(df2, 1, max)
  df2$MIN <- apply(df2, 1, min)
  df2 <- cbind(STNAME = census_df$STNAME, df2)
  df2$ABS <- abs(df2$MAX - df2$MIN)
  df2 <- aggregate(ABS ~ STNAME, df2, sum)
  df3 <- subset(df2, ABS == max(ABS))  
  df3 <- as.character(df3$STNAME)
  df3
}

answer_seven()
[1] "Texas"
```
Питання 8
В census_df США поділені на 4 регіони (колонка "REGION"). Напишіть функцію,
яка знаходить округи (county), що належать регіонам 1 або 2, назва яких
починається з "Washington" та POPESTIMATE2015 більше ніж POPESTIMATE2014.
Функція повинна повернути 5х2 дата фрейм з колонками "STNAME", "CTYNAME".
```{r}
answer_eight <- function() {
    df1 <- subset(census_df, (census_df$REGION == 1 | census_df$REGION == 4) & census_df$POPESTIMATE2015 > census_df$POPESTIMATE2014 & census_df$STNAME == "Washington")[1:5,c("STNAME", "CTYNAME")]
    df1
}

answer_eight()
         STNAME        CTYNAME
3001 Washington     Washington
3002 Washington   Adams County
3004 Washington  Benton County
3005 Washington  Chelan County
3006 Washington Clallam County
```
