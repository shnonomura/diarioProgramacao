# Java interface

Interfaces definem e PADRONIZAM como coisas, pessoas e sistemas podem interar entre si. Por exemplo, os controles em um rádio servem
como uma interface entre o usuário do rádio e os componentes internos do rádio. Os controles permitem que os usuários realizem uma 
série limitada de operações (aumentar o volume, mudar de estação, ligar e desligar o rádio e etc).

A interface especifica quais operações um rádio deve permitir que os usuários realizem, mas não especifica como essas operações são
realizadas.

Objetos de software também se comunicam por interfaces.

Uma declaração de interface inicia com a palavra-chave _interface_ e contém SOMENTE _constantes e métodos abstratos_. Diferentemente
das classes , todos os membros de interface devem ser public e as interfaces não podem especificar nenhum detalhe de implementação,
tais como, declarações de método concreto e variáveis de instâncias.

**Declaração da interface Payable**

	public interface Payable{
	
		double getPaymentAmount();
	
	}

As interfaces oferecem uma capacidade que classes NÃO RELACIONADAS permitam implementar conjunto de métodos gerais ABSTRATOS COMUNS.

	Todos os métodos declarados em uma interface são implicitamente _public abstract_ e todos os campos são implicitamente 
	public, static e final.

## Usando uma interface

<image src="https://github.com/shnonomura/diarioProgramacao/blob/master/imagem/hierarquia interface.jpg">