# RecyclerView

O widget RecyclerView é uma versão mais avançada do ListView.

No RecyclerView diferentes componentes trabalham juntos para exibir os dados.

É um objeto que é adicionado ao Layout.

É preenchido com visualizações fornecidas por um GERENCIADOR DE LAYOUT definido pelo programador (ex., LinearLayoutManager ou GridLayoutManager). Tais visualizações são representadas por objetos de visualização em que cada um é responsável em exibir uma única visualização. Por exemplo, se sua lista mostra uma coletânea de músicas, cada objeto de visualização pode representar um único álbum.

O RecyclerView cria apenas quantos fixadores de visualização forem necessários para exibir a parte da tela do conteúdo dinâmico, além de alguns extras. À medida que o usuário rola a lista, o RecyclerView retira as visualizações da tela e as vincula novamente aos dados que estão rolando na tela. 

Os Objetos de visualização são instâncias de uma classe que deve ser definida estendendo Recycler.ViewHolder.
