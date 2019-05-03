Лабораторна робота № 5

Для лабораторної роботи необхідно завантажити zip файл з даними за
посиланням:
«https://www.dropbox.com/s/i9wi47oyhfb7qlh/rprog_data_specdata.zip?dl=0».
Це файл містить 332 csv файлів, що містять у собі результати спостережень за забрудненням повітря дрібнодисперсними частками (fine particular matter air pollution) у 332 локаціях у США. Кожен файл містить дані з одного монітору. ID номер кожного монітору міститься у назві файлу. Наприклад, дані з монітору під номером 200 містяться у файлі «200.csv». Кожен файл містить три змінні:
Data: дата спостереження в форматі (рік-місяць-день), sulfate: рівень
сульфатних часток в повітрі на дату (мікрограми на кубічний метр) та nitrate:
рівень нітратних часток в повітрі на дату (мікрограми на кубічний метр). Для цій роботи необхідно додати на Github файл pmean.R, який містить усі функції. В файлі md необхідно указати виклик функції з аргументами та вивід у консоль результатів роботи функцій.

1. Написати функцію pmean, яка обчислює середнє значення (mean)
забруднення сульфатами або нітратами серед заданого переліка
моніторів. Ця функція приймає три аргументи: «directory», «pollutant»,
«id». Directory – папка, в якій розміщені дані, pollutant – вид забруднення,
id – перелік моніторів. Аргумент id має значення за замовчуванням 1:332.
Функція повинна ігнорувати NA значення. 


```{r}
getwd()
[1] "D:/Documents"

path = "D:/Documents/specdata"
out.file <- ""
file.names <- dir(path, pattern =".csv")
file.names
  [1] "001.csv" "002.csv" "003.csv" "004.csv" "005.csv" "006.csv"
  [7] "007.csv" "008.csv" "009.csv" "010.csv" "011.csv" "012.csv"
 [13] "013.csv" "014.csv" "015.csv" "016.csv" "017.csv" "018.csv"
 [19] "019.csv" "020.csv" "021.csv" "022.csv" "023.csv" "024.csv"
 [25] "025.csv" "026.csv" "027.csv" "028.csv" "029.csv" "030.csv"
 [31] "031.csv" "032.csv" "033.csv" "034.csv" "035.csv" "036.csv"
 [37] "037.csv" "038.csv" "039.csv" "040.csv" "041.csv" "042.csv"
 [43] "043.csv" "044.csv" "045.csv" "046.csv" "047.csv" "048.csv"
 [49] "049.csv" "050.csv" "051.csv" "052.csv" "053.csv" "054.csv"
 [55] "055.csv" "056.csv" "057.csv" "058.csv" "059.csv" "060.csv"
 [61] "061.csv" "062.csv" "063.csv" "064.csv" "065.csv" "066.csv"
 [67] "067.csv" "068.csv" "069.csv" "070.csv" "071.csv" "072.csv"
 [73] "073.csv" "074.csv" "075.csv" "076.csv" "077.csv" "078.csv"
 [79] "079.csv" "080.csv" "081.csv" "082.csv" "083.csv" "084.csv"
 [85] "085.csv" "086.csv" "087.csv" "088.csv" "089.csv" "090.csv"
 [91] "091.csv" "092.csv" "093.csv" "094.csv" "095.csv" "096.csv"
 [97] "097.csv" "098.csv" "099.csv" "100.csv" "101.csv" "102.csv"
[103] "103.csv" "104.csv" "105.csv" "106.csv" "107.csv" "108.csv"
[109] "109.csv" "110.csv" "111.csv" "112.csv" "113.csv" "114.csv"
[115] "115.csv" "116.csv" "117.csv" "118.csv" "119.csv" "120.csv"
[121] "121.csv" "122.csv" "123.csv" "124.csv" "125.csv" "126.csv"
[127] "127.csv" "128.csv" "129.csv" "130.csv" "131.csv" "132.csv"
[133] "133.csv" "134.csv" "135.csv" "136.csv" "137.csv" "138.csv"
[139] "139.csv" "140.csv" "141.csv" "142.csv" "143.csv" "144.csv"
[145] "145.csv" "146.csv" "147.csv" "148.csv" "149.csv" "150.csv"
[151] "151.csv" "152.csv" "153.csv" "154.csv" "155.csv" "156.csv"
[157] "157.csv" "158.csv" "159.csv" "160.csv" "161.csv" "162.csv"
[163] "163.csv" "164.csv" "165.csv" "166.csv" "167.csv" "168.csv"
[169] "169.csv" "170.csv" "171.csv" "172.csv" "173.csv" "174.csv"
[175] "175.csv" "176.csv" "177.csv" "178.csv" "179.csv" "180.csv"
[181] "181.csv" "182.csv" "183.csv" "184.csv" "185.csv" "186.csv"
[187] "187.csv" "188.csv" "189.csv" "190.csv" "191.csv" "192.csv"
[193] "193.csv" "194.csv" "195.csv" "196.csv" "197.csv" "198.csv"
[199] "199.csv" "200.csv" "201.csv" "202.csv" "203.csv" "204.csv"
[205] "205.csv" "206.csv" "207.csv" "208.csv" "209.csv" "210.csv"
[211] "211.csv" "212.csv" "213.csv" "214.csv" "215.csv" "216.csv"
[217] "217.csv" "218.csv" "219.csv" "220.csv" "221.csv" "222.csv"
[223] "223.csv" "224.csv" "225.csv" "226.csv" "227.csv" "228.csv"
[229] "229.csv" "230.csv" "231.csv" "232.csv" "233.csv" "234.csv"
[235] "235.csv" "236.csv" "237.csv" "238.csv" "239.csv" "240.csv"
[241] "241.csv" "242.csv" "243.csv" "244.csv" "245.csv" "246.csv"
[247] "247.csv" "248.csv" "249.csv" "250.csv" "251.csv" "252.csv"
[253] "253.csv" "254.csv" "255.csv" "256.csv" "257.csv" "258.csv"
[259] "259.csv" "260.csv" "261.csv" "262.csv" "263.csv" "264.csv"
[265] "265.csv" "266.csv" "267.csv" "268.csv" "269.csv" "270.csv"
[271] "271.csv" "272.csv" "273.csv" "274.csv" "275.csv" "276.csv"
[277] "277.csv" "278.csv" "279.csv" "280.csv" "281.csv" "282.csv"
[283] "283.csv" "284.csv" "285.csv" "286.csv" "287.csv" "288.csv"
[289] "289.csv" "290.csv" "291.csv" "292.csv" "293.csv" "294.csv"
[295] "295.csv" "296.csv" "297.csv" "298.csv" "299.csv" "300.csv"
[301] "301.csv" "302.csv" "303.csv" "304.csv" "305.csv" "306.csv"
[307] "307.csv" "308.csv" "309.csv" "310.csv" "311.csv" "312.csv"
[313] "313.csv" "314.csv" "315.csv" "316.csv" "317.csv" "318.csv"
[319] "319.csv" "320.csv" "321.csv" "322.csv" "323.csv" "324.csv"
[325] "325.csv" "326.csv" "327.csv" "328.csv" "329.csv" "330.csv"
[331] "331.csv" "332.csv"

length(file.names)
[1] 332

pmean <- function(directory, pollutant, id=1:332){
  file.names <- dir(path=directory, pattern =".csv", full.names=TRUE)
  values <- numeric()
  for (i in id){
    df <- read.csv(file.names[i])
    values <- c(values, df[[pollutant]])
  }
  mean(values, na.rm=TRUE)
}
pmean('specdata', 'sulfate', 1:332)
[1] 3.189369

pmean('specdata', 'sulfate', 1:10)
[1] 4.064128

pmean("specdata", "nitrate", 1:332)
[1] 1.702932


```
2. Написати функцію complete, яка виводить кількість повних спостережень
(the number of completely observed cases) для кожного файлу. Функція
приймає два аргументи: «Directory» та «id» та повертає data frame, в
якому перший стовпчик – ім’я файлу, а другий – кількість повних
спостережень. 

```{r}
complete <- function(directory, id=1:332){
  file.names <- dir(path=directory, pattern =".csv", full.names=TRUE)
  dataframe <- data.frame() 
  for (i in id){
    df <- read.csv(file.names[i]) 
    observations <- sum(complete.cases(df)) 
    df1 <- data.frame(i, observations) 
    dataframe <- rbind(dataframe, df1)
  }
colnames(dataframe) <- c("id", "observations") 
dataframe
}

complete("specdata", 1)
  id observations
1  1          117

complete("specdata", c(2, 4, 8, 10, 12))
1  2         1041
2  4          474
3  8          192
4 10          148
5 12           96


```
3. Написати функцію corr, яка приймає два аргументи: directory (папка, де
знаходяться файли спостережень) та threshold (порогове значення, за
замовчуванням дорівнює 0) та обчислює кореляцію між сульфатами та
нітратами для моніторів, кількість повних спостережень для яких більше
порогового значення. Функція повинна повернути вектор значень
кореляцій. Якщо ні один монітор не перевищує порогового значення,
функція повинна повернути numeric вектор довжиною 0. Для обчислення
кореляції між сульфатами та нітратами використовуйте вбудовану функцію 
«cor» з параметрами за замовчуванням.


```{r}

corr <- function(directory, threshold = 0) {
  file.names <- dir(path=directory, pattern =".csv", full.names=TRUE)
  result <- c()
	for (i in 1:332) {
		df <- read.csv(file.names[i])
		df <- df[complete.cases(df),]
		if (nrow(df) > threshold) {
			result <- c(result, cor(df$sulfate, df$nitrate))
		}
	}
	return(result)
}
	


cr <- corr("specdata", 150)
head(cr); summary(cr)

[1] -0.01895754 -0.14051254 -0.04389737 -0.06815956 -0.12350667
[6] -0.07588814
    Min.  1st Qu.   Median     Mean  3rd Qu.     Max. 
-0.21060 -0.04999  0.09463  0.12530  0.26840  0.76310 

cr <- corr("specdata", 400)
head(cr); summary(cr)
[1] -0.01895754 -0.04389737 -0.06815956 -0.07588814  0.76312884
[6] -0.15782860
    Min.  1st Qu.   Median     Mean  3rd Qu.     Max. 
-0.17620 -0.03109  0.10020  0.13970  0.26850  0.76310 

cr <- corr("specdata", 5000)
head(cr); summary(cr) ; length(cr)
NULL
Length  Class   Mode 
     0   NULL   NULL 
[1] 0

```
