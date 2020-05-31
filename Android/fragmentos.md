# Fragmentos - realização de transacões com fragmentos


fonte: 
1. https://www.youtube.com/watch?v=i22INe14JUc
2. https://developer.android.com/guide/components/fragments.html#UI
3. https://developer.android.com/guide/components/fragments.html#Adding
4. https://developer.android.com/guide/components/fragments.html#Transactions

Um fragmento é geralmente usado como parte de uma interface do usuário da atividade e contribui para a atividade com o próprio layout.

Para fornecer um layout para um fragmento, você deve implementar o método de callback onCreateView(), que o sistema Android chama no momento em que o fragmento precisa desenhar o layout. A implementação desse método deve retornar uma View, que é a raiz do layout do fragmento.

Geralmente, um fragmento contribui com a atividade do host com uma parte da IU, que é incorporada como parte da hierarquia de visualizações geral da atividade. Há duas formas de adicionar um fragmento ao layout da atividade:

*- Declarar o fragmento dentro do arquivo de layout da atividade.*

Neste caso, é possível especificar as propriedades do layout para o fragmento como se fosse uma visualização. Por exemplo, veja o arquivo de layout para uma atividade com dois fragmentos:

	<?xml version="1.0" encoding="utf-8"?>
	<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
	    android:orientation="horizontal"
	    android:layout_width="match_parent"
	    android:layout_height="match_parent">
	    <fragment android:name="com.example.news.ArticleListFragment"
		    android:id="@+id/list"
		    android:layout_weight="1"
		    android:layout_width="0dp"
		    android:layout_height="match_parent" />
	    <fragment android:name="com.example.news.ArticleReaderFragment"
		    android:id="@+id/viewer"
		    android:layout_weight="2"
		    android:layout_width="0dp"
		    android:layout_height="match_parent" />
	</LinearLayout>

O atributo android:name em <fragment> especifica a classe Fragment a instanciar no layout.

Quando o sistema cria esse layout de atividade, ele instancia cada fragmento especificado no layout e chama o método onCreateView() para cada um para recuperar o layout de cada fragmento. O sistema insere a View retornada pelo fragmento diretamente no lugar do elemento <fragment>.

	Observação: cada fragmento requer um identificador único que o sistema possa usar para restaurá-lo se a atividade for reiniciada (e que possa ser usado para capturar o fragmento para realizar transações como a remoção). Há duas formas de fornecer um código a um fragmento.

	    Fornecer o atributo android:id com um código exclusivo.
	    Fornecer o atributo android:tag com uma string exclusiva.

*- Ou adicionar programaticamente o fragmento a um ViewGroup existente.*

A qualquer momento, enquanto a atividade está em execução, é possível adicionar fragmentos ao layout da atividade. Basta especificar um ViewGroup no qual posicionar o fragmento.


Um grande recurso fornecido por fragmentos em atividades é a possibilidade de *adicionar, remover, substituir e realizar outras ações* com eles em resposta à interação do usuário. Cada *conjunto de alterações realizadas na atividade é chamado de transação* e cada alteração pode ser feita usando APIs em FragmentTransaction.

Também é possível *salvar cada transação em uma pilha de retorno gerenciada pela atividade*, permitindo que o usuário navegue inversamente pelas alterações de fragmento (semelhante à navegação inversa pelas atividades).

É possível adquirir uma instância de *FragmentTransaction do FragmentManager* da seguinte forma:

	FragmentManager fragmentManager = getSupportFragmentManager();
	FragmentTransaction fragmentTransaction = fragmentManager.beginTransaction();

Cada transação é um conjunto de alterações que você quer realizar ao mesmo tempo. É possível definir todas as alterações desejadas para uma transação usando métodos como add(), remove() e replace(). Em seguida, para aplicar a transação à atividade, chame commit().

_Antes de chamar commit(), no entanto, você pode querer chamar addToBackStack() para adicionar a transação a uma pilha de retorno de transações de fragmentos_. *A pilha de retorno é gerenciada pela atividade* e permite que o usuário retorne ao estado anterior do fragmento ao pressionar o botão Voltar.

Por exemplo, veja como você pode substituir um fragmento por outro e preservar o estado anterior da pilha de retorno:

	// Create new fragment and transaction
	Fragment newFragment = new ExampleFragment();
	FragmentTransaction transaction = getSupportFragmentManager().beginTransaction();

	// Replace whatever is in the fragment_container view with this fragment,
	// and add the transaction to the back stack
	transaction.replace(R.id.fragment_container, newFragment);
	transaction.addToBackStack(null);

	// Commit the transaction
	transaction.commit();

Neste exemplo, newFragment substitui qualquer fragmento (se houver) que estiver no contêiner do layout identificado pelo código R.id.fragment_container. Ao chamar addToBackStack(), a transação de substituição é salva na pilha de retorno para que o usuário possa reverter a transação e voltar ao fragmento anterior pressionando o botão Voltar.

Em seguida, FragmentActivity recupera automaticamente os fragmentos da pilha de retorno por meio de onBackPressed().

Se você adicionar várias alterações à transação — como outra add() ou remove() — e chamar addToBackStack(), todas as alterações aplicadas antes de chamar commit() serão adicionadas à pilha de retorno como uma única transação, e o botão Voltar reverterá todas elas ao mesmo tempo.

A ordem em que você adiciona as alterações em FragmentTransaction não importa, exceto nas situações a seguir:

- Você precise chamar commit() por último.
- Você esteja adicionando vários fragmentos ao mesmo contêiner. Nesse caso, a ordem de inclusão determinará a ordem em que eles aparecerão na hierarquia de visualização.

	Se você não chamar addToBackStack() ao realizar uma transação que remove um fragmento, ele será destruído quando a transação estiver confirmada e o usuário não poderá navegar de volta a ele. No entanto, se você chamar addToBackStack() ao remover um fragmento, ele será interrompido e retomado posteriormente, caso o usuário navegue de volta a ele.

	Dica: para cada transação de fragmento, é possível aplicar uma animação de transição chamando setTransition() antes da realização.

Ao chamar commit(), a transação não será realizada de imediato. Em vez disso, o parâmetro agenda a execução no thread de IU da atividade (o thread “main”, ou principal) assim que possível. Se necessário, no entanto, é possível chamar executePendingTransactions() do thread de IU para executar imediatamente as transações enviadas por commit(). Essa medida geralmente não é necessária, a não ser que a transação represente uma dependência para jobs em outros threads.

	Atenção: é possível realizar uma transação usando commit() somente antes da atividade salvar o estado (quando o usuário deixa a atividade). Caso tente efetivar as alterações após esse ponto, uma exceção será lançada. Isso acontece porque o estado após a efetivação pode ser perdido se a atividade precisar ser restaurada. Para situações em que não há problema em perder a confirmação, use commitAllowingStateLoss().




