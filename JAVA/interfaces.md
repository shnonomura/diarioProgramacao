# Java interface

fonte: Java como programar - 10ª edição - editora Pearson - autores: Paul Deitel/Harvey Deitel


Interfaces definem e PADRONIZAM como coisas, pessoas e sistemas podem interagir entre si. Por exemplo, os controles em um rádio servem
como uma interface entre o usuário do rádio e os componentes internos do rádio. Os controles permitem que os usuários realizem uma 
série limitada de operações (aumentar o volume, mudar de estação, ligar e desligar o rádio e etc).

A interface especifica quais operações um rádio deve permitir que os usuários realizem, mas não especifica como essas operações são
realizadas.

Objetos de software também se comunicam por interfaces.

Uma declaração de interface inicia com a palavra-chave _interface_ e contém SOMENTE _constantes e métodos abstratos_. Diferentemente
das classes , todos os membros de interface devem ser public e as interfaces não podem especificar nenhum detalhe de implementação,
tais como, declarações de método concreto e variáveis de instâncias.

**Declaração da interface Payable**
      
      // Declaração da interface Payable
	public interface Payable{
	
		double getPaymentAmount();
	
	}

As interfaces oferecem uma capacidade que classes NÃO RELACIONADAS permitam implementar conjunto de métodos gerais ABSTRATOS COMUNS.

	Todos os métodos declarados em uma interface são implicitamente public abstract e todos os campos são implicitamente 
	public, static e final.

## Usando uma interface

O diagrama de classes da UML da figura abaixo mostra a interface e a hierarquia de classes utilizadas em uma aplicativo. A hierarquia
inicia com a interface Payable. A UML separa uma interface de outras classes colocando a palavra "interface" entre o
símbolo de aspas francesas (<< e >>) acima do nome da interface. A UML expressa o relacionamento entre uma classe e uma interface por
meio de um relacionamento conhecido como _realização_. Diz-se que uma classe _realiza_ ou _implementa_, os métodos de uma interface.

Um diagrama de classe modela uma realização com uma seta tracejada com uma ponta oca apontando da implementação da classe para a 
interface. O diagrama indica que as classes Invoice e Employee implementam a interface Payable. Como no diagrama da figura, a classe
Employee aparece em _itálico_, indicando que é uma classe ABSTRATA. A classe concreta SalariedEmployee estende Employee herdando seu
relacionamento de realização da superclasse com a interface Payable.

<image src="https://github.com/shnonomura/diarioProgramacao/blob/master/imagem/hierarquia interface.jpg">

	1. Uma classe JAVA só pode extender UMA classe, mas pode implementar várias interfaces.
	2. Todas as classes extende implicitamente Object.
	3. Implementar uma interface é como assinar um contrato com o compilador que afirma "Irei declarar todos os métodos 
	   especificados pela interface ou irei declarar minha classe como abstract.

A classe Employee implementa Payable, assim podemos dizer que um Employee _é uma Payable_. Isto é, objetos de quaisquer classes que 
estendem Employee também são objetos Payable. Objetos SalariedEmployee são objetos Payable.

	Os objetos de quaisquer subclasses da classe que implementa a interface também pode ser pensados como
	objetos-interface.
	
	Portanto, assim como podemos atribuir a referência de um objeto SalariedEmployee a uma variável superclasse Employee,
	TAMBÉM PODEMOS ATRIBUIR a referência de um objeto SalariedEmployee a uma variável da interface Payable.
	
	Invoice implementa Payable, portanto um objeto Invoice também é um objeto Payable, e podemos atribuir a referência
	de um objeto Invoice a uma variável Payable.

### Observação: 

	A variável de um tipo de interface deve referenciar um objeto para chamar métodos e
	todo os objetos têm métodos da classe OBJECT.

Ex.: o exemplo abaixo, cria Array Payable Objects e popula a array com os objetos que implementan a interface Payable (Invoice e
     SalariedEmployee) e através de um for processa cada elemento polimorficamente.
	
	// Payable interface test program processing Invoices and 
      // Employees polymorphically.
      public class PayableInterfaceTest 
      {
         public static void main(String[] args)
         {
            // create four-element Payable array
            Payable[] payableObjects = new Payable[4];
            
            // populate array with objects that implement Payable
            payableObjects[0] = new Invoice("01234", "seat", 2, 375.00);
            payableObjects[1] = new Invoice("56789", "tire", 4, 79.95);
            payableObjects[2] = 
               new SalariedEmployee("John", "Smith", "111-11-1111", 800.00);
            payableObjects[3] = 
               new SalariedEmployee("Lisa", "Barnes", "888-88-8888", 1200.00);

            System.out.println(
               "Invoices and Employees processed polymorphically:"); 

            // generically process each element in array payableObjects
            for (Payable currentPayable : payableObjects)
            {
               // output currentPayable and its appropriate payment amount
               System.out.printf("%n%s %n%s: $%,.2f%n", 
                  currentPayable.toString(), // could invoke implicitly
                  "payment due", currentPayable.getPaymentAmount()); 
            } 
         } // end main
      } // end class PayableInterfaceTest

