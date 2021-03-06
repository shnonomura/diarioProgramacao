
# Activities

_fonte: https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/unit-1-get-started/lesson-2-activities-and-intents/2-1-c-activities-and-intents/2-1-c-activities-and-intents.html_

**Uma activity representa uma simples tela do seu aplicativo cuja a interface o usuário pode interagir**. Por exemplo, um app de email poderia ter uma
atividade que mostra a lista de novos emails, outra atividade para criar um email, uma outra atividade para ler as mensagens. O nosso aplicativo
é uma coleção de activity que nós, próprios, criamos ou que fazemos uso em outros aplicativos.

Embora as activity em nosso aplicativo trabalhe em conjunto de forma coesa, **cada activity é independente uma da outra**. Isto possibilita nosso aplicativo iniciar uma atividade em outro aplicativo, bem como, permite que outros aplicativos inicie uma _activity_ em nosso aplicativo (claro, se o aplicativo permitir)_. Por exemplo, uma aplicativo de mensagens poderia iniciar uma activity no aplicativo câmera para tirar uma foto e depois iniciar uma activity no aplicativo de email de forma a compartilhar a imagem via email.

<image src="https://github.com/shnonomura/diarioProgramacao/blob/master/imagem/activities%20em%20acao.JPG">

Geralmente, uma _activity_ em uma aplicativo é especificado como a 'main' activity (MainActivity). O usuário visualiza a _MainActivity_ quando é iniciado o aplicativo pela primeira vez. Cada _activity_ pode startar outras _activity_ para exeutar diferentes ações.

Cada vez que uma nova _activity_  é iniciada, a anterior é interrompida, mas o sistema android mantém a _activity_ em uma pilha (a "back stack"). Quando o usuário finaliza a _activity_ atual e pressiona o botão _Back_, a _activity_ é popped (retirada) da pilha e destruída, e a _activity_ anterior é executada.

Quando uma _activity_ é interrompida porque uma nova _activity_ foi iniciada, a primeira _activity_ é notificada pelos métodos **activity  lifecycle callback**.
A _activity lifecycle_ corresponde a um conjunto de estados que a _activity_ pode se encontrar:

    - quando a _activity_ é criada pela primeira vez;
    - quando está parada ou em execução;
    - quando o sistema a destrói.

