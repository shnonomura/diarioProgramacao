# Classe abstrata x inteface

<small>_fonte: Java - Como programar - 10ª edição - Paul Deitel, Harvey Deitel - Editora Pearson Education do Brasil Ltda_</small>


O Java suporta coleções de métodos relacionados que normalmente permitem informar aos objetos **O QUE FAZER**, mas **NÃO COMO FAZER**. Na analogia do carro, uma interface ensina o que fazer para o carro andar por meio do volante, acelerador, cambio e freios do objeto carro. Por meio dessa interface podemos dizer o que o objeto carro deve fazer, mas não como deve fazê-lo. Outro exemplo, os controles de um rádio  servem de interface entre o usuários e os elementos que fazem funcionar e emitir os sons capturados pela antena do rádio POR MEIO do botão de sintonia, de volume e de ligar e desligar o rádio.

Como as interfaces, de certa forma, determinam, definem, estabelecem _O QUE FAZER_ elas padronizam como as coisas, pessoas e sistemas podem interagir entre si por meio de MÉTODOS .

  Uma interface deve ser utilizada quando **NÃO há campo, nem método padrão a implementar*. O Java permite que
  *classes NÃO RELACIONADAS** implementem um _conjunto de métodos comuns_. Ex.: permite , calcular pagamentos
  devidos a funcionários e faturas em um único aplicativo, polimorficamente.

<image src="https://github.com/shnonomura/diarioProgramacao/blob/master/Java/java-interfaces.jpg">

Todos os métodos e campos declarados em uma interface **são métodos PUBLIC ABSTRACT e os campos PUBLIC STATIC FINAL, implicitamente.** Tanto o é, que é boa prática de programação Java não declarar os termos public e abstract aos métodos da interface. Da mesma forma, para os campos da interface a não declaração dos termos public, static e final.
