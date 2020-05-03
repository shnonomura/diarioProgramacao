# Android - AsyncTask

***fontes:***
	1. _[Guia para o processamento em segundo plano](https://developer.android.com/guide/background#challenges_in_background_processing) - acessado em 2020-05-02_
	2. _documentação do classe AsyncTask disponível no Android Studio._

Cada app para Android tem uma linha de execução principal encarregada de gerenciar a IU, coordenar interações de usuários e receber eventos de ciclo de vida. Se houver muito trabalho nessa linha de execução, o app poderá travar ou ficar mais lento, levando a uma experiência de usuário indesejável. Qualquer cálculo e operação de longa duração, como decodificar bitmaps, acessar o disco ou executar solicitações de rede, precisa ser feito em uma linha de execução separada em segundo plano. Em geral, tudo que leve mais do que alguns milissegundos precisa ser delegado a uma linha de execução em segundo plano. Pode ser necessário que algumas tarefas sejam realizadas enquanto o usuário interage ativamente com o app. Para saber como executar tarefas em linhas de execução em segundo plano e fora da linha de execução de IU principal ()enquanto o app está sendo usado ativamente

A **classe AsyncTask** possibilita um meio fácil de controlar a UI Thread. Ela permite executar operações em background e apresentar os resultados na UI Threadsem ter que manipular threads e/ou handlers.

**Asynctask** foi projetado para auxiliar as classes Thread e Handler. É ideal para operações de curta duração (uns poucos segundos no máximo). _Se for durar mais do que isso é recomendado usar as várias API fornecidas pelo pacote java.util.concurrent tais como Executor, ThreadExecutor e FutureTask_.

Uma AsyncTask é executada em background e seu resultado é publicado na UI Thread que controla as views da activity (tela). 
A definição de uma AsyncTask é feita por meio de 3 tipos genéricos de tarefas:

	1. Params
	2. Progress
	3. Result
	
E quatro passos/métodos:

	1. preExecute
	2. doInBackground
	3. onProgressUpdate
	4. onPostExecute


```java
public abstract class AsyncTask<Params, Progress, Result> { 
.....
}
```
A Classe AsyncTask para ser utilizada, ela deve ser extendida por meio de uma classe que o desenvolvedor criará.
A Subclasse MyAsyncTask (por exemplo) sobrescreverá pelo menos um método _doInBackground_ (para executar a tarefa desejada) e mais frequentemente um segundo método, o método _onPostExecute_ (para postar na UI pela UI Thread o resultado desejado).


Segue _um exemplo de uma subclasse gerada_.

```java
	private class DownloadFilesTask extends AsyncTask <URL, Integer, Long>; {
		protected Long doInBackground(URL... urls) {
			int count = urls.length;
			long totalSize = 0;
			for (int i = 0; i &lt; count; i++) {
				totalSize += Downloader.downloadFile(urls[i]);
				publishProgress((int) ((i / (float) count)100));
				// Escape early if cancel() is called
				if (isCancelled()) break;
			}
			return totalSize;
		}

		protected void onProgressUpdate(Integer... progress) {
			setProgressPercent(progress[0]);
		}

		protected void onPostExecute(Long result) {
			showDialog("Downloaded " + result + " bytes");
		}
	}
```

Um vez criada, a tarefa é executada de forma simples utilizando o seguinte comando:

```java
	new DownloadFilesTask().execute(url1, url2, url3);
```
 
 ## AsyncTask's generic types
 
Os três tipos de tarefas assíncronas utilizadas são as seguintes:


	1. PARAMS, os tipos de parâmetros a serem enviados para a tarefas
	2. PROGRESS, os tipos de unidades a ser apresentada que indicam o andamento da tarefa em execução.
	3. RESULT, os tipos de resultados esperados.


Nem todos os tipos são sempre utilizados pelas tarefas assíncronas. Para definir os tipos que não serão utilizados,
basta utilizar o tipo _void_.

private class MyTask extends AsyncTask<void, void, void> { ... }

## Os 4 métodos
Quando uma tarefa assíncrona é executada, a tarefa passa por 4 métodos:


	1. onPreExecute()  é invocado a UI Thread antes da tarefa ser executada. Este passo é normalmente utilizado para
	configurar a tarefa mostrando uma barra de progresso na interface do usuário, por exemplo.

	2. doInBackground() é invocado sob a thread secundária imediatamente após o término da _onPreExecute_. Este passo
	é utilizado para realizar os procedimentos em background e que pode levar um bom tempo. Os parâmetros da tarefa
	assíncrona são passadas para este passo. O resultado da processamento será retornado para este passo que enviará
	para o último passo. Este passo pode utilizar o _publishProgress_ para apresentar uma ou mais unidades do progresso.
	Tais valores são apresentados pela UI Thread no passo _onProgressUpdade_.

	3. onProgressUpdate() é invocado sob a UI Thread secundária após a chamada à _publishProgress_. A duração da execução 
	é indefinida. Este método é utilizado para mostrar qualquer forma de _progressão_ na interface do usuário enquanto o 
	processamento computational está em execução. Por exemplo, pode ser utilizado para animar uma barra de progresso ou 
	mostrar logs em um campo texto.

	4. onPostExecute() é invocado a UI Thread depois de finalizado o processamento em background. O resultado para este
	método é passado por parâmetro.


 ## Cancelando a tarefa

Uma tarefa pode ser cancelada a qualquer hora invocando o método _cancel(boolean)_. Invocar este método causará subsequentes
chamadas para _isCancelled()_ que retorna _true_.

Depois de invocar esse método _cancel(boolean)_, o método _onCancelled(Object)_, será invocado depois do retorno de
_doInBackground(object)_, ao invés de _onPostExecute(Object)_.

Para assegurar que uma tarefa está cancelada tão logo quanto possível, deve-se checar sempre a o valor de retorno
de _isCancelled_ periodicamente a partir de _doInBackground(Object)_, se possível ( de dentro de um loop, por exemplo).

## Regras do Threading

Há algumas poucas regras que devem ser seguidas para a Classe AsyncTask trabalhar propriamente:

	1. a classe AsyncTask deve ser carregada a **partir a da UI Thread**. Isto é feito automaticamente a partir
	versão _JELLY_BEAN_.

	2. a instância da AsyncTask deve ser criada sob a UI Thread.

	3. o método execute() deve ser invocado pela UI Thread.

	4. **Não chamar** os métodos _onPreExecute, onPostExecute, doInBackground e onProgressUpdate_ **manualmente**.

	5. a tarefa só pode ser executada somente uma única vez. Uma exceção será lançada, se for acionada um segunda execução.

## Acompanhamento da memória

AsyncTask garante que todas as chamadas callback estejam sincronizadas para assegurar conforme segue, sem explicitar sincronizações.


	1. Os efeitos da memória correspondentes ao método onPreExecute() e tudo mais executado antes da chamada para o método execute(),
	incluindo a construção do objeto AsyncTask, são visíveis ao método doInBackground().

	2. Os efeitos da memória correspondentes ao método doInBackground() que precede a chamada ao método publishProgress(),
	são visíveis à chamada ao método onProgressUpdate(). Mas o método doInBackground() continua a sua execução, e cuidados devem
	ser tomados de forma que atualizações posteriores do método doInBackground() não interfira em uma chamada em progresso do
	método onProgressUpdate().

	3. Os efeitos da memória que precedem a chamada ao método cancel(), são visíveis após uma chamada ao método isCancelled() que
	retorna _true_ com resultado, ou durante ou após uma chamada para método onCancelled().


## Ordem de execução

As AsyncTasks eram executadas de forma serial sob o controle de uma simples thread em background.
Na versão Donut, foi alterado permitindo múltiplas tarefas serem executadas em paralelo.
Com a HoneyComb, as tarefas passaram a ser executadas sob o controle de uma simples thread para evitar todos erros comuns de aplicações
causados pela execução em paralelo.

Se o desenvolvedor deseja realmente a execução em paralelo, deve-se utilizar o método executeOnExecutor (java.util.concurrent.Executor)
com  a THREAD_POOL_EXECUTOR.

```java 
public abstract class AsyncTask<Params, Progress, Result> {
    private static final String LOG_TAG = "AsyncTask";

    // We keep only a single pool thread around all the time.
    // We let the pool grow to a fairly large number of threads if necessary,
    // but let them time out quickly. In the unlikely case that we run out of threads,
    // we fall back to a simple unbounded-queue executor.
    // This combination ensures that:
    // 1. We normally keep few threads (1) around.
    // 2. We queue only after launching a significantly larger, but still bounded, set of threads.
    // 3. We keep the total number of threads bounded, but still allow an unbounded set
    //    of tasks to be queued.
    private static final int CORE_POOL_SIZE = 1;
    private static final int MAXIMUM_POOL_SIZE = 20;
    private static final int BACKUP_POOL_SIZE = 5;
    private static final int KEEP_ALIVE_SECONDS = 3;

    private static final ThreadFactory sThreadFactory = new ThreadFactory() {
        private final AtomicInteger mCount = new AtomicInteger(1);

        public Thread newThread(Runnable r) {
            return new Thread(r, "AsyncTask #" + mCount.getAndIncrement());
        }
    };

}
```