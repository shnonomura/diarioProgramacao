# Dados - Persistência de dados

"Segundo o artigo da Wikipedia: [O que é persistência de dados?](https://pt.stackoverflow.com/questions/140411/o-que-%C3%A9-persist%C3%AAncia-de-dados)

    É característica de um _ESTADO_ que sobrevive ao processo que o criou. Sem essa capacidade, o estado só existiria na RAM, e seria perdido quando a RAM parasse (desligando-se o computador, por exemplo).

É só um nome bonito pra dizer que gravou os dados em algum lugar e que não se perderá quando o computador for desligado (HDD, SSD, ou até na nuvem, por exemplo). É só uma forma de dizer que o dado ficará disponível "para sempre" sem dizer como.

Normalmente está ligado a banco de dados, mas é claro que não precisa ser em um, qualquer tipo de aplicação que grave qualquer coisa para que esse _ESTADO_ possa ser recuperado mais tarde está fazendo persistência. Não é algo ligado ao SQL, mas é claro que o SQL faz persistências, especialmente em INSERT, UPDATE e DELETE.

É um paradoxo dizer que o DELETE faz persistência de dados, ( rsrs ) mas esta certo, de fato, faz. Faz a persistência de meu desejo de que esse dado seja excluído.

É isso mesmo, persistência é sobre o estado e não sobre o dado em si. Dizer que o dado não existe mais é uma mudança de estado que precisa ser persistida. Inclusive porque não é só apagar, ele grava rastros de que isto foi feito (pelo menos em banco de dados costuma ocorrer, mas mesmo que não ocorresse, ainda valia)." 

_fonte: https://pt.stackoverflow.com/questions/140411/o-que-%C3%A9-persist%C3%AAncia-de-dados_