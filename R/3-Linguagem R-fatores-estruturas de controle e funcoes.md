# criando vetores
vec1 <- c(1001,1002,1003,1004,1005)
vec2 <- c(0,1,1,0,2)
vec3 <- c('verde', 'laranja', 'azul', 'laranja', 'verde')

# by joining the vectors in a data frame
df <- data.frame(vec1, vec2,vec3)
df

# verificando que o R categorizou a última coluna como fator
str(df)

# verificando os níveis do fator. Perceba que os níveis estão categorizados
levels(df$vec3)

#criando outra coluna e atribuindo labels
df$cat1 <- factor(df$vec3, labels = c("cor2", "cor1", "cor3"))
df$cat1
df

# internamente, os fatores são registrados como inteiros, mas a ordenação
# segue a ordem alfabética das strings
str(df)

      veja como foi feita a atribuição Azul = cor2 , Laranja = cor1 , Verde = cor3 , ou seja, os vetores com os labels, 
      seguiram a ordem alfabética dos níveis classificados pelo R.

# Criando outra coluna e atribuir labels
# Ao aplicarmos a  função factor() à coluna vec2, internamente R classificou
# em ordem alfabética e quando atribuímos os labels, foi feita a associação.

df$cat2 <- factor(df$vec2, labels = c("Divorciado", "Casado", "Solteiro"))
df
str(df)
levels(df$cat2)

# 3.Linguagem R - fatores, estruturas de controle e funções

# BigDataAzure/cap10/10-expressoes_regulares.RStudio

## busca os pacotes carregados
search()

## instala e carrega pacotes - posso criar um vetor que contém os pacotes desejados
install.packages(c("ggvis","tm","dplyr"))
library("ggvis")

## desinstala a biblioteca
detach(package:dplyr)

## listar conteúdo dos pacotes
ls(pos = "package:tm")

## lista as funcoes de um pacote
lsf.str("package:tm")

## carregar a biblioteca
library(MASS)

## visualizar o conteúdo da dataset (conjunto de dados)
head(iris)
tail(iris)
summary(iris)
iris$Sepal.Length
sum(Sepal.Length)

## criar pacotes R usando o RStudio

Para testar os pacotes que você criar, será necessário instalar estes 2 pacotes abaixo:

	install.packages('testthat')
	install.packages('devtools')

Você  pode  criar  seus  pacotes  R  usando  apenas  o  RStudio.
Entretanto, dependendo dos recursos que serão usados no seu pacote,
você precisa instalar as ferramentas de desenvolvimento para pacotes
R, de acordo com seu sistema operacional:

**Windows**

Baixar o Rtools:

	https://cran.rstudio.com/bin/windows/Rtools

Baixar o LaTeX:

	http://miktex.org/download

## expressoes regulares - encontra um padrao dentro de um vetor e permite substituicao

- grep(pattern, x, ignore.case = FALSE, perl = FALSE, value = FALSE, fixed = FALSE, useBytes = FALSE, invert = FALSE)
- grepl(pattern, x, ignore.case = FALSE, perl = FALSE, fixed = FALSE, useBytes = FALSE)
- sub(pattern, replacement, x, ignore.case = FALSE, perl = FALSE, fixed = FALSE, useBytes = FALSE)
- gsub(pattern, replacement, x, ignore.case = FALSE, perl = FALSE, fixed = FALSE, useBytes = FALSE)
- regexpr(pattern, text, ignore.case = FALSE, perl = FALSE, fixed = FALSE, useBytes = FALSE)
- gregexpr(pattern, text, ignore.case = FALSE, perl = FALSE, fixed = FALSE, useBytes = FALSE)

str <- c("Expressões", "regulares", "em linguagem R",
         "permitem a busca de padrões", "e exploração de textos",
         "podemos buscar padrões em dígitos",
         "como por exemplo",
         "10992451280")

### c é um vetor de strings
str <- c("Expressões", "regulares", "em linguagem R",
         "permitem a busca de padrões", "e exploração de textos",
         "podemos buscar padrões em dígitos",
         "como por exemplo",
         "10992451280")

 - encontra o padrao "ex" dentro de str e retorna a posição.

	grep("ex",str,value=F)

- encontra o padrão "ex" dentro de str e retorna a strings

	grep("ex",str,value=F)

- encontra a posição onde há digitos (\\d) dentro str

	grep("\\d", str , value = F)

- encontra a posição onde há digitos (\\d) dentro str e retorna a string

	grep("\\d", str , value = T)

- retorna true ou false quando pesquisa o vetor character. Retorna true, a posição que tem dígito. O mais, indica inclusive outro caractere.

	grepl("\\d+", str)

- retorna true, a posição que NÃO tem dígito. O mais, indica inclusive outro caractere.

	grepl("\\D+", str)

## gsub - substitui o string por outro dentro do vetor character

gsub("em", "***" , str)
gsub("ex","EX",str,ignore.case = T)

## sub - variação de gsub

sub("em","EM",str)

## regexpr encontra um padrão em uma string
frase <- "É uma string"
regexpr(pattern = "u", frase)

## gregexpr é uma variação de regexpr()
gregexpr(pattern="u", frase)

## com as funcoes acima, pode-se substituir, excluir e alterar um vetor character
str2 <- c("2678 é maior que 45 - @??!§$" , "Vamos escrever 14 scripts R")


- gsub("\\d","", str2)

	[1] " é maior que  - @??!§$"   
	[2] "Vamos escrever  scripts R"

- gsub("\\D","",str2)

	[1] "267845" "14"   

- gsub("\\s","",str2)

	[1] "2678émaiorque45-@??!§$"
	[2] "Vamosescrever14scriptsR"

- gsub("[iot]","Q",str2)

	[1] "2678 é maQQr que 45 - @??!§$"
	[2] "VamQs escrever 14 scrQpQs R"

- gsub("[[:punct:]]","", str2)

	[1] "2678 é maior que 45  "      
	[2] "Vamos escrever 14 scripts R"

# Datas e Hora

## Hora e Data do sistema
hoje <- Sys.Date()
hoje
class(hoje)
Sys.time()
Sys.timezone()


## Data - representada por Date
Armazenados como número de dias desde 1 de Janeiro de 1970

## Time - representado por POSIXct
Armazenados como número de segundos desde 1 de Janeiro de 1970

## Formatando Datas
- %d: dia do mês em 2 dígitos (13)
- %m: mês em 2 digitos (01)
- %y: ano em 2 dígitos (82)
- %Y: ano em 4 dígitos (1982)
- %A: dia da semana (Friday)
- %a: dia da semana abreviado (Fri)
- %B: mês (July)
- %b: mês abreviado (Jul)


## Formatando hora
- %H: hora (00-23)
- %M: minuto
- %S: segundo
- %T: formado reduzido para %H:%M:%S
?strptime


## Formatando a saída - as.Date()
as.Date("2018-06-28")
as.Date("Jun-28-18", format = "%b-%d-%y")
as.Date("28 Jun, 2018", format = "%d %B, %Y")


## Função format()
Sys.Date()
?format
format(Sys.Date(), format = "%d %B, %Y")
format(Sys.Date(), format = "Hoje é %A!")


## Convertendo Datas - as.POSIXct
date1 <- "Jun 13, '96 hours:23 minutes:01 seconds:45"
date1_convert <- as.POSIXct(date1, format = "%B %d, '%y hours:%H minutes:%M seconds:%S")
date1_convert


## Operações com Datas
data_de_hoje <- as.Date("2016-06-25", format = "%Y-%m-%d")
data_de_hoje
data_de_hoje + 1

my_time <- as.POSIXct("2016-05-14 11:24:134")
my_time
my_time + 1

data_de_hoje - as.Date(my_time)
data_de_hoje - my_time

**necessário fazer conversão de datas para mesmo tipo para realizar cálculos**

data_de_hoje - as.Date(my_time)


## Convertendo Data em formato específico
O vetor de números pode representar o número de dias, horas ou minutos (de acordo com o que você quer converter)
A Linguagem R considera o ponto de início a data de 01 de Janeiro de 1970 e contabiliza o total
de horas, minutos ou segundos, aquilo que o vetor numérico representar

dts = c(1127056501,1104295502,1129233601,1113547501,1119826801,1132519502,1125298801,1113289201)

mydates = dts

## POSIXct
Armazena os segundos desde uma data específica, convertendo os valores numéricos (que podem representar horas, minutos ou segundos) desde 01 de Janeiro de 1970

## POSIXt é a classe principal e POSIXct e POSIXlt são subclasses.
Poderíamos usar aqui apenas POSIXct, que é a subclasse (mas não podemos usar apenas a classe principal)

class(mydates) = c('POSIXt','POSIXct')

mydates

class(mydates)

mydates = structure(dts, class = c('POSIXt','POSIXct'))
mydates


## Função ISODate
b1 = ISOdate(2011,3,23)
b1
b2 = ISOdate(2012,9,19)
b2
b2 - b1

difftime(b2, b1, units = 'weeks')


## Pacote lubridate
?lubridate
install.packages("lubridate")
require(lubridate)

**informa uma string e retorna uma date**
ymd("20180604")
mdy("06-04-2018")
dmy("04/06/2018")



chegada <- ymd_hms("2016-06-04 12:00:00", tz = "Pacific/Auckland")

partida <- ymd_hms("2011-08-10 14:00:00", tz = "Pacific/Auckland")

chegada

partida

second(chegada)

second(chegada) <- 23

chegada

wday(chegada)

wday(chegada, label = TRUE)

class(chegada)

## Cria um objeto que especifica a data de início e data de fim

interval(chegada, partida)


tm1.lub <- ymd_hms("2020-05-24 23:55:26")
tm1.lub

tm2.lub <- mdy_hm("05/25/20 08:32")
tm2.lub

year(tm1.lub)
week(tm1.lub)

tm1.dechr <- hour(tm1.lub) + minute(tm1.lub)/60 + second(tm1.lub)/3600
tm1.dechr
force_tz(tm1.lub, "Pacific/Auckland")

## Gerando um dataframe de datas

sono <- data.frame(bed.time = ymd_hms("2013-09-01 23:05:24", "2013-09-02 22:51:09",
                                       "2013-09-04 00:09:16", "2013-09-04 23:43:31",
				       "2013-09-06 00:17:41", "2013-09-06 22:42:27",
                                       "2013-09-08 00:22:27"), rise.time = ymd_hms("2013-09-02 08:03:29", "2013-09-03 07:34:21",
                                                                                   "2013-09-04 07:45:06", "2013-09-05 07:07:17", "2013-09-06 08:17:13", "2013-09-07 06:52:11",
                                                                                   "2013-09-08 07:15:19"), sleep.time = dhours(c(6.74, 7.92, 7.01, 6.23, 6.34, 7.42, 6.45)))

sono

sono$eficiencia <- round(sono$sleep.time/(sono$rise.time - sono$bed.time) * 100, 1)

sono

## Gerando um plot a partir de datas

par(mar = c(5, 4, 4, 4))

plot(round_date(sono$rise.time, "day"), sono$eficiencia, type = "o", col = "blue", xlab = "Manhã", ylab = NA)

par(new = TRUE)

plot(round_date(sono$rise.time, "day"), sono$sleep.time/3600, type = "o", col = "red", axes = FALSE, ylab = NA, xlab = NA)

axis(side = 4)

mtext(side = 4, line = 2.5, col = "red", "Duração do Sono")

mtext(side = 2, line = 2.5, col = "blue", "Eficiência do Sono")
