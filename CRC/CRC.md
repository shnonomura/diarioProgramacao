# CRC - Cyclic Redundance Check

A **verificação cíclica de redundância (do inglês, CRC - Cyclic Redundancy Check)** _é um método de detecção de erros normalmente usada em redes digitais e dispositivos de armazenamento para detectar mudança acidental em cadeias de dados_. Mensagens de dados enviado aos sistemas recebem um pequeno anexo com um valor de verificação baseado no resto de divisão polinomial do seu conteúdo. No ato da recuperação do dado o cálculo é refeito e comparado com o valor gerado anteriormente. Se os valores não se mostrarem semelhantes podem ser aplicadas ações para correção de dados, evitando assim a corrupção de dados. CRC pode ser usada para correção de erros a partir de alguns métodos.

A verificação cíclica de redundância é amplamente utilizada em dispositivos binários por ser de simples implementação, é matematicamente fácil de ser analisada e apresenta bons resultados na detecção de erros comuns em canais de transmissão causados por ruído. A função utilizada para gerar o valor de verificação possui tamanho fixo, e é utilizada igualmente como uma função hash.

O primeiro a propor a CRC foi W. Wesley Peterson em 1961. Hoje, a 32-bit CRC function of Ethernet e vários outros padrões são trabalhos de vários pesquisadores e foi publicada em 1975. 

## Aplicações

	Um dispositivo CRC-enabled calcula uma pequena sequência binária de tamanho fixo, conhecido como código de verificação ou CRC, para cada mensagem que será enviada ou recebida e a anexa aos dados, formando uma palavra-código (codeword).

	Quando uma palavra código é recebida ou lida, o dispositivo compara seu código de verificação anexado com um novo ,calculado a partir da mensagem, ou aplica o CRC sobre toda a palavra-código e compara o resultado com uma constante residual pré-definida.

	Se os códigos CRC não são semelhantes a mensagem contém erros de dados. O dispositivo pode realizar ações corretivas como reler a mensagem ou requisitar um novo envio da mesma.

	Senão os dados podem ser tratados como corretos e sem erro. (Com uma pequena probabilidade o código pode conter erros não detectados; essa é a natureza fundamental da verificação de erros ).

## Integridade dos dados

Os códigos de verificação cíclica de redundância são projetados para proteger contra erros típicos dos canais de comunicação, onde podem garantir a integridade de mensagens de forma rápida e confiável. Entretanto, eles não são aplicáveis para proteção contra alteração intencional de dados.

Não há nenhum tipo de **autenticação**, um invasor pode editar a mensagem e recalcular seu código de verificação sem que a substituição seja detectada. Quando as funções criptográficas de hash e a CRC são armazenadas em conjunto com os dados, elas não podem proteger contra alterações intencionais dos dados. Aplicações que requerem tal proteção devem usar mecanismos de autenticação criptográficas assinaturas digitais ou códigos de autenticação da mensagem.

_fonte: CRC - https://pt.wikipedia.org/wiki/CRC . Acessado em 16/04/2020._
