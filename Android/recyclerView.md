# RecyclerView

O objeto *widget RecyclerView* é uma versão mais avançada do ListView que é adicionada a um Layout.

No RecyclerView diferentes componentes trabalham juntos para exibir os dados.

É preenchido com visualizações fornecidas por um GERENCIADOR DE LAYOUT definido pelo programador (ex., LinearLayoutManager ou GridLayoutManager). Tais visualizações são representadas por objetos de visualização em que cada um é responsável em exibir uma única visualização. Por exemplo, se sua lista mostra uma coletânea de músicas, cada objeto de visualização pode representar um único álbum.

O RecyclerView cria apenas quantos objetos de visualização forem necessários para exibir a parte da tela do conteúdo dinâmico, além de alguns extras. À medida que o usuário rola a lista, o RecyclerView retira as visualizações da tela e as vincula novamente aos dados que estão rolando na tela. 

Os *objetos de visualização* são INSTÂNCIAS de uma *classe extendida da _Recycler.ViewHolder_*. E são GERENCIADOS por um *adapter extendido da classe RecyclerView.Adapter*. O adapter cria os objetos de visualização conforme necessário. Ainda, o adapter vincula os objetos de visualização aos respectivos dados.Isso é feito atribuindo ao objeto de visualização com base na posição do dado fornecido por uma lista. Determinando assim, qual dado deve ser apresentado ao acionar o método onBindViewHolder() do adapter.

Esse modelo RecyclerView realiza diversas otimizações para que você não precise fazer isso:

    Quando a lista é preenchida pela primeira vez, ela cria e vincula alguns fixadores de visualização em ambos os lados da lista. Por exemplo, se a visualização estiver exibindo as posições de lista de 0 a 9, o RecyclerView criará e vinculará esses fixadores de visualização e também poderá criar e vincular o fixador de visualização para a posição 10. Dessa forma, se o usuário rolar a lista, o próximo elemento estará pronto para ser exibido.
    
	À medida que o usuário rola a lista, o RecyclerView cria novos fixadores de visualização conforme necessário. Ele também salva os fixadores de visualização que rolaram para fora da tela para que possam ser reutilizados. Se o usuário mudar a direção que estava rolando, os fixadores de visualização que foram rolados para fora da tela poderão ser trazidos de volta. Por outro lado, se o usuário continuar rolando na mesma direção, os fixadores de visualização que estiverem fora da tela por mais tempo poderão ser redefinidos para novos dados. O fixador de visualização não precisa ser criado ou ter sua visualização ampliada; em vez disso, o app apenas atualiza o conteúdo da visualização para corresponder ao novo item ao qual estava vinculada.
    
	Quando os itens exibidos mudarem, você poderá notificar o adaptador chamando um método RecyclerView.Adapter.notify…() apropriado. O código integrado do adaptador vincula novamente apenas os itens afetados.
