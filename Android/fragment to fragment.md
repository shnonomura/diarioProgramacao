# Fragment to Fragment - Activity comunication

fonte:  
1. https://developer.android.com/training/basics/fragments/communicating
2. https://www.youtube.com/watch?v=i22INe14JUc

Para reutilizar os componentes da IU de fragmento, você precisa construí-los como componentes completamente autossuficientes e modulares, que definam o próprio layout e comportamento. Assim que tiver definido esses fragmentos reutilizáveis, é possível associá-los a uma atividade e conectá-los à lógica do app para abranger a IU composta em sua totalidade.

Na maioria das vezes, é recomendável que um fragmento se comunique com outro, para, por exemplo, alterar o conteúdo baseado em um evento do usuário. Toda a comunicação entre fragmentos é feita por meio de um ViewModel compartilhado ou da atividade associada. Dois fragmentos nunca devem comunicar-se diretamente.

A maneira recomendada de estabelecer a comunicação entre fragmentos é criar um objeto ViewModel compartilhado. Ambos os fragmentos podem acessar o ViewModel por meio da atividade contida. Os fragmentos podem atualizar dados no ViewModel e, se os dados forem expostos usando o LiveData, o novo estado será enviado para o outro fragmento, desde que ele esteja observando o LiveData no ViewModel. Para saber como implementar esse tipo de comunicação, leia a seção "Compartilhar dados entre fragmentos" no guia do ViewModel.

Caso não consiga usar um ViewModel compartilhado para realizar a comunicação entre seus fragmentos, é possível implementar um fluxo de comunicação manualmente usando interfaces. Contudo, essa implementação é mais trabalhosa e não é facilmente reutilizável em outros fragmentos. 

## LifeCycle

Lifecycle

Though a Fragment's lifecycle is tied to its owning activity, it has its own wrinkle on the standard activity lifecycle. It includes basic activity lifecycle methods such as onResume(), but also important are methods related to interactions with the activity and UI generation.

The core series of lifecycle methods that are called to bring a fragment up to resumed state (interacting with the user) are:

    - onAttach(Activity) called once the fragment is associated with its activity.
    - onCreate(Bundle) called to do initial creation of the fragment.
    - onCreateView(LayoutInflater, ViewGroup, Bundle) creates and returns the view hierarchy associated with the fragment.
    - onActivityCreated(Bundle) tells the fragment that its activity has completed its own Activity#onCreate.
    - onViewStateRestored(Bundle) tells the fragment that all of the saved state of its view hierarchy has been restored.
    - onStart() makes the fragment visible to the user (based on its containing activity being started).
    - onResume() makes the fragment begin interacting with the user (based on its containing activity being resumed). 

As a fragment is no longer being used, it goes through a reverse series of callbacks:

    - onPause() fragment is no longer interacting with the user either because its activity is being paused or a fragment operation is modifying it in the activity.
    - onStop() fragment is no longer visible to the user either because its activity is being stopped or a fragment operation is modifying it in the activity.
    - onDestroyView() allows the fragment to clean up resources associated with its View.
    - onDestroy() called to do final cleanup of the fragment's state.
    - onDetach() called immediately prior to the fragment no longer being associated with its activ