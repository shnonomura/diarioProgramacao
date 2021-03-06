# Fundamento: Android - Thread

Cada aplicativo em execução corresponde um processo. E cada processo posso ter várias linhas de execução, ou seja, várias threads.
As threads são subsistemas dentro de um processo que executam uma ou mais tarefas. E cada uma das Thread trabalha de forma independente.

<image src="https://github.com/shnonomura/diarioProgramacao/blob/master/imagem/processo_e_thread.jpg">

_fonte: Curso Desenvolvimento Android Completo 2020 - Crie 18 Apps - Jamilton Damasceno_

**Todo o processo tem uma Thread principal (UI Thread)**. A UI Thread é responsável pela interação com o usuário e é controlada pelo OS (Operational System) do Android. Ainda, a UI Thread não precisa ser criada haja visto que ao ser iniciado o processo ela é criada automativamente. Contudo, qualquer outra thread deve ser criada pelo desenvolvedor.

Pode-se enviar códigos diretamente para a UI Thread, mas tem que se ter o cuidado de não sobrecarregar a UI Thread haja visto que provocar o travamento/interrupção do processo ou aplicativo. Para que isso não ocorra, o desenvolvedor deve criar sua própria Thread. Se a UI thread for bloqueada por mais de 5 segundos aproximadamente, o usuário receberá a mensagem  "application not responding" (ANR). E o usuário poderá decidir abandonar sua aplicação ou pior decidir desinstalá-lo.

<image src="https://github.com/shnonomura/diarioProgramacao/blob/master/imagem/UI_Thread.jpg">

_fonte: Curso Desenvolvimento Android Completo 2020 - Crie 18 Apps - Jamilton Damasceno_

O UI thread é onde o nosso aplicativo interage com os componentes dos pacotes android.widget e android.view.

O pacote android.widget contém os elementos que são usados nas telas do aplicativo (maioria, visuais).
O pacote android.view fornece as classes que manipulam o layout das telas e que possibilitam a interação com o usuário.


As funções da UI Thread são:

	. renderizar tela
	. processar eventos (por ex.: clique de um botão)
	. atender activities
	. broadcast receivers
	. services
	
<image src="https://github.com/shnonomura/diarioProgramacao/blob/master/imagem/funcoes_da_UI_Thread.jpg">

_fonte: Curso Desenvolvimento Android Completo 2020 - Crie 18 Apps - Jamilton Damasceno_

A criação de uma thread pode ser feita: extendendo a classe Thread ou utilizando a interface runnable.
 
<image src="https://github.com/shnonomura/diarioProgramacao/blob/master/imagem/como_criar_uma_Thread.jpg">

_fonte: Curso Desenvolvimento Android Completo 2020 - Crie 18 Apps - Jamilton Damasceno_

	.Referências: Curso Desenvolvimento Android Completo 2020 - Crie 18 Apps - Jamilton Damasceno
	.AsyncTask and AsyncTaskLoader - acessado em 11/04/2020 - 
	 https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/unit-3-working-in-the-background/lesson-7-background-tasks/7-1-c-asynctask-and-asynctaskloader/7-1-c-asynctask-and-asynctaskloader.html#uithread