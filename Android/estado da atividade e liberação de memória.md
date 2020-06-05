# Estado da atividade e liberação de memória

fonte: https://developer.android.com/guide/components/activities/activity-lifecycle?hl=pt-br#asem

O sistema elimina processos quando precisa liberar RAM. A probabilidade de o sistema eliminar um determinado processo depende do estado do processo no momento. O estado do processo, por sua vez, depende do estado da atividade em execução no processo. A tabela 1 mostra a correlação entre o estado do processo, o estado da atividade e a probabilidade de o sistema eliminar o processo. 

<image src="https://github.com/shnonomura/diarioProgramacao/blob/master/imagem/ciclo%20de%20vida%20e%20estado%20da%20atividade.JPG">

O sistema nunca elimina uma atividade diretamente para liberar memória. Em vez disso, ele elimina o processo em que a atividade opera, destruindo não só a atividade, mas também todo o restante em execução no processo. Para saber como preservar e restaurar os estados da IU da atividade quando ocorre o processo de eliminação iniciado pelo sistema, consulte Como salvar e restaurar o estado da atividade.

Um usuário também pode eliminar um processo usando o Gerenciador de aplicativos em “Configurações” para eliminar o aplicativo correspondente.

Para mais informações sobre o processo em geral, consulte Processos e threads. Para saber mais sobre como o ciclo de vida de um processo está ligado aos estados das atividades nele, consulte a seção Ciclo de vida dos processos nessa página. 

# Como salvar e restaurar o estado transitório da IU

Um usuário espera que o estado da IU de uma atividade permaneça o mesmo durante uma alteração na configuração, como rotação ou mudança para o modo de várias janelas. No entanto, o sistema destrói a atividade por padrão quando ocorre uma mudança de configuração. Isso exclui qualquer estado de IU armazenado na instância da atividade. Da mesma forma, um usuário espera que o estado da IU permaneça o mesmo se ele alternar temporariamente do seu aplicativo para outro e retornar ao inicial posteriormente. No entanto, o sistema pode destruir o processo do aplicativo enquanto o usuário estiver ausente e a atividade será interrompida.

Quando a atividade é destruída devido a limitações do sistema, use uma combinação de ViewModel, onSaveInstanceState() e/ou armazenamento local para preservar o estado transitório da IU do usuário. Para saber mais sobre as expectativas do usuário em relação ao comportamento do sistema e como preservar melhor os dados complexos do estado da IU nas atividades iniciais pelo sistema e eliminação do processo, consulte Como salvar o estado da IU.

Essa seção destaca qual o estado da instância e como implementar o método onSaveInstance(), que é por si só um callback na atividade. Se os dados da IU forem simples e leves, como um tipo de dados primitivo ou um objeto simples (como String), você poderá usar o onSaveInstanceState() sozinho para manter o estado da IU nas mudanças de configuração e na eliminação do processo iniciada pelo sistema. Na maioria dos casos, entretanto, recomendamos o uso do ViewModel e do onSaveInstanceState() (como destacado em Como salvar o estado da IU), uma vez que o onSaveInstanceState() incorre em custos de serialização/desserialização.
Estado da instância

Há alguns casos em que a atividade é destruída devido ao comportamento normal do aplicativo, como quando o usuário pressiona o botão Voltar ou a atividade sinaliza a própria destruição chamando o método finish(). Quando a atividade é destruída porque o usuário pressionou o botão Voltar ou a atividade em si é finalizada, o conceito do sistema e do usuário dessa instância Activity se perde. Nesses cenários, a expectativa do usuário corresponde ao comportamento do sistema, e você não tem trabalho extra.

No entanto, se o sistema destruir a atividade devido a limitações dele mesmo (como uma mudança na configuração ou pressão sobre a memória), embora a instância Activity real tenha se perdido, o sistema recordará a existência dela. Se o usuário tentar navegar de volta para a atividade, o sistema criará uma nova instância dela usando um conjunto de dados salvos que descrevem o estado da atividade quando ela foi destruída.

Os dados salvos usados pelo sistema para restaurar o estado anterior são chamados de estados de instância e são uma coleção de pares de chave-valor armazenados no objeto Bundle. Por padrão, o sistema usa o estado da instância Bundle para salvar informações sobre cada objeto View no layout da atividade (como o valor de texto inserido em um widget EditText). Assim, se a instância da atividade for destruída e recriada, o estado do layout será restaurado para o estado anterior sem que haja necessidade de código. No entanto, a atividade pode conter mais informações de estado do que se quer restaurar, como variáveis de associação que rastreiam o progresso do usuário na atividade.

	Observação: para que o sistema Android restaure o estado das visualizações na atividade, 
	cada uma delas precisa ter um código exclusivo, fornecido pelo atributo android:id.	

Um objeto Bundle não é adequado para preservar mais do que uma quantidade trivial de dados, pois requer serialização no thread principal e consome memória do processo do sistema. Para preservar mais do que uma quantidade muito pequena de dados, use uma abordagem combinada para preservar dados, com armazenamento local, o método onSaveInstanceState() e a classe ViewModel, conforme destacado em Como salvar estados da IU. 