# 3.Linguagem R - fatores, estruturas de controle e funções

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

# gsub - substitui o string por outro dentro do vetor character

gsub("em", "***" , str)
gsub("ex","EX",str,ignore.case = T)

# sub - variação de gsub

sub("em","EM",str)

# regexpr encontra um padrão em uma string
frase <- "É uma string"
regexpr(pattern = "u", frase)

# gregexpr é uma variação de regexpr()
gregexpr(pattern="u", frase)

# com as funcoes acima, pode-se substituir, excluir e alterar um vetor character
str2 <- c("2678 é maior que 45 - @??!§$" , "Vamos escrever 14 scripts R")


> gsub("\\d","", str2)
[1] " é maior que  - @??!§$"   
[2] "Vamos escrever  scripts R"

> gsub("\\D","",str2)
[1] "267845" "14"   
 
> gsub("\\s","",str2)
[1] "2678émaiorque45-@??!§$" 
[2] "Vamosescrever14scriptsR"

> gsub("[iot]","Q",str2)
[1] "2678 é maQQr que 45 - @??!§$"
[2] "VamQs escrever 14 scrQpQs R" 

> gsub("[[:punct:]]","", str2)
[1] "2678 é maior que 45  "      
[2] "Vamos escrever 14 scripts R"
