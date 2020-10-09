# Sockets

<image src="https://github.com/shnonomura/diarioProgramacao/blob/master/imagem/Socket.jpg">

_figura 1 -  sockets - https://www.treinaweb.com.br/blog/uma-introducao-a-tcp-udp-e-sockets_

A Java API para WebSocket é que fornece suporte para criação de aplicações WebSocket.
WebSocket é um protocolo de aplicação que fornece comunicação full-duplex (recebe e  envia dados) entre dois pontos através do protocolo TCP.

No modelo tradicional de requesição-resposta usado no HTTP, o cliente realiza requisições e o servidor responde a elas. A troca é sempre inicializada pelo cliente; o servidor não pode enviar qualquer dado sem que o cliente requisite primeiramente. Este modelo trabalhou bem para World Wide Web (internet)
quando cliente realizava requisições por documentos que sofriam mudanças ocasionais, mas as  limitações foram se tornando relevantes a partir do momento que os documentos mudavam rapidamente e os usuários desejavam maior interatividade com a Web. O protocolo WebSocket lida com essas limitações fornecendo um canal de comunicação entre o cliente e o servidor. Combinado com outras tecnologias, tais como JavaScript e HTML5, WebSocket permite as aplicações entregar uma experiência mais rica ao usuário. 

Em uma aplicação WebSocket, o servidor publica um ponto WebSocket, e o cliente usa o URI de nó para conectar-se ao servidor. O Protocolo WebSocket apresenta
as mesmas funções para ambos os nós uma vez que a comunicação for estabelecida. O cliente e servidor podem enviar mensagens de um para o outro a qualquer hora, enquanto a conexão estiver aberta. O encerramento pode ser executado a qualquer hora. Clientes geralmente conectam-se somente a um servidor e servidores aceitam conexões de vários clientes ao mesmo tempo.

O protocolo WebSocket tem duas partes: o handshake e o data transfer ( o aperto de mãos e a transferência de dados). O clientes inicializa o handshake enviando uma requisição ao nó WebSocket do servidor utilizando a sua URI (endereço eletrônico. ex: www.google.com).

O handshake é compatível com uma estrutura baseada no Http. Os servidores web interpretando como uma requisição de conexão Http. Um exemplo de handshake na visão do cliente se para como:

	GET /path/to/websocket/endpoint HTTP/1.1
	Host: localhost
	Upgrade: websocket
	Connection: Upgrade
	Sec-WebSocket-Key: xqBt3ImNzJbYqRINxEFlkg==
	Origin: http://localhost
	Sec-WebSocket-Version: 13
	
Um exemplo de handshake a partir do servidor em resposta à requisição do cliente parece-se com:

	HTTP/1.1 101 Switching Protocols
	Upgrade: websocket
	Connection: Upgrade
	Sec-WebSocket-Accept: K7DJLdLooIwIG/MOpvWFB3y3FE8=


Nós WebSocket são representados por URI que apresentam a seguinte forma:

	ws://host:port/path?query
	wss://host:port/path?query

O esquema *ws* representa um conexão não encriptada e o esquema *wss* representa uma conexão encriptada. O componente _port_ é opcional.
 
	port 80 -> conexões não encriptadas
	port 443 -> conexõa encriptada
	
O componente _path_ indica a localização do nó do servidor. O componente _query_ é opcional.

<image src="https://github.com/shnonomura/diarioProgramacao/blob/master/imagem/Portos.jpg">

_figura 2 - portos dos nós - https://www.treinaweb.com.br/blog/uma-introducao-a-tcp-udp-e-sockets_

_fonte: 18 Java API for WebSocket - Java Documentation - https://docs.oracle.com/javaee/7/tutorial/websocket.htm#GKJIQ5_
