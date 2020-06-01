# SOAP - Simple Object Access Protocol

<img src="https://github.com/shnonomura/diarioProgramacao/blob/master/imagem/soap.png">

**SOAP (Simple Object Access Protocol, em português Protocolo Simples de Acesso a Objetos)** _é um protocolo_ para troca de informações estruturadas em uma _plataforma descentralizada e distribuída_. É um dos padrões para o desenvolvimento de web services ( há também, o REST ou RESTFul).

	Os Web Services são utilizados como uma forma de integração e comunicação de sistemas, de modo que um sistema possa realizar uma chamada para um serviço de outro sistema a fim de obter informações. Estas chamadas podem enviar e receber informações em diversos formatos, sendo XML e JSON os mais conhecidos atualmente.

	Uma das grandes vantagens na construção de web services é que eles permitem acessar os serviços de forma padronizada e independente de linguagem de programação. Por exemplo, é possível escrever um web service com a linguagem Java, mas consumí-lo em qualquer outra linguagem, tais como C#, PHP, Python e etc.
	
	Existem várias formas de criar web services sendo os mais conhecidos o SOAP ou REST (Representational State Transfer).
	
	A WSDL de todo web service é um grande XML que descreve todos os métodos disponíveis neste serviço, ou seja, os métodos que podemos chamar e executar. Com estas informações, qualquer sistema independente de linguagem de programação pode fazer chamadas nestes web services, pois neste arquivo está descrito exatamente como estas chamadas devem ser feitas.
	
A WSDL de todo web service é um grande XML que descreve todos os métodos disponíveis neste serviço, ou seja, os métodos que podemos chamar e executar. Com estas informações, qualquer sistema independente de linguagem de programação pode fazer chamadas nestes web services, pois neste arquivo está descrito exatamente como estas chamadas devem ser feitas.

Como o SOAP é um grande XML, ele começou a perder espaço para web services RESTful que apresentam uma sintaxe mais enxuta e podem enviar e receber informações em formatos mais leve. Principamente no mundo mobile.

O protocolo de comunicação SOAP de web services é descrito por uma WSDL (Web Services Description Language).
Para seu formato de mensagem utiliza-se do XML (Extensible Markup Language).
Na prática, o SOAP é um grande arquivo XML trafegado entre os sistemas para fazer a comunicação.

Na camada de aplicação do modelo OSI, utiliza-se dos protocolos RPC e HTTP para negociação e transmissão de mensagens, respectivamente.

<img src="https://github.com/shnonomura/diarioProgramacao/blob/master/imagem/web_service_soap.JPG">

_Web Services SOAP em Java - 2ª Edição: Guia prático para o desenvolvimento - Autor : Daniel Adorno Gomes_

O protocolo para negociação de _chamadas de procedimento remoto (RPC -Remote Procedure Calls)_ consiste em chamar um procedimento em outro programa por uma rede (ex.: a internet). Normalmente, estes protocolos são independentes da linguagem permitindo que um programa cliente escrito em C++ chame um servidor de banco de dados remoto escrito em Java sem que qualquer um dos lados saibam a linguagem empregada pelas partes.

O protocolo de transmissão de mensagens _HTTP - Hipertext Transfer Protocol_ é o protocolo empregado na internet. Para toda transação web realizada o protocolo HTTP é invocado. HTTP está por trás de qualquer requisição para qualquer documento web ou gráfico, cada clique de hipertexto e para toda requisição de um formulário. Ele é útil porque fornece um modo padronizado para os computadores se comunicarem entre si.

**Referências**
_1.Web Services SOAP em Java - 2ª Edição: Guia prático para o desenvolvimento - Daniel Adorno Gomes_
\_2. SOAP - https://pt.wikipedia.org/wiki/SOAP . Acessado em 10/04/2020._
_3. Web Services RESTFul - 1ª Edição - Novatec - Ricardo R. Lecheta._
