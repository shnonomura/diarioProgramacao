# Transmitir dados entre destinos

O componente de navegação permite que você anexe dados a uma operação de navegação definindo argumentos para um destino. Por exemplo, um destino de perfil de usuário pode usar um argumento de ID do usuário para determinar qual usuário exibir.

Em geral, recomendamos que você dê preferência para a transmissão da quantidade mínima de dados entre destinos. Por exemplo, transmita uma chave para recuperar um objeto em vez de transmitir o próprio objeto, já que o espaço total para todos os estados salvos é limitado no Android. Se você precisar transmitir grandes quantidades de dados, use um ViewModel, conforme descrito em Compartilhar dados entre fragmentos.

# Definir argumentos de destino

Para transmitir dados entre destinos, primeiro defina o argumento adicionando-o ao destino que o recebe seguindo estas etapas:

    - No Navigation Editor, clique no destino que recebe o argumento.
    - No painel Attributes, clique em Add (+).
    - Na janela Add Argument Link que é exibida, insira o nome do argumento, o tipo dele, se ele é anulável e um valor padrão, se necessário.
    - Clique em Add. O argumento aparecerá na lista Arguments no painel Attributes.
    - Clique na ação correspondente que o leva a esse destino. No painel Attributes, você verá seu argumento recém-adicionado na seção Argument Default Values.

Veja que o argumento foi adicionado em XML. Clique na guia Text para alternar para a visualização XML e observe que seu argumento foi adicionado ao destino que o recebe. Veja um exemplo abaixo:

	<fragment android:id="@+id/myFragment" >
		<argument
		     android:name="myArg"
		     app:argType="integer"
		     android:defaultValue="0" />
	</fragment>

# Tipos de argumentos compatíveis

A biblioteca Navigation é compatível com os seguintes tipos de argumento:

<image src="https://github.com/shnonomura/diarioProgramacao/blob/master/imagem/Android/tipos de argumentos.jpg">