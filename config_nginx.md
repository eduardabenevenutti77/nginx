Na sexta-feira, dia 16/08/24, tive a chance de mergulhar no universo da configuração do NGINX e explorar o aproveitamento das suas funcionalidades, como proxy reverso e web server.

🛠️ O Poder do NGINX
O NGINX é uma ferramenta desenvolvida em C, que opera em baixo nível e se integra diretamente à aplicação.
  
nginx.conf: 
  O arquivo nginx.conf é a espinha dorsal da configuração do NGINX. Ele funciona quase como uma linguagem de programação, permitindo que a gente utilize variáveis, includes, e configure parâmetros importantes para o funcionamento do servidor.
   
    📌 Alguns Parâmetros Essenciais:
  
  •	user nginx: Define o usuário do sistema operacional que executará o NGINX. Esse usuário é criado automaticamente na instalação, mas pode ser alterado conforme necessário.
  
  •	worker_processes auto: Controla quantos processos serão executados pelos worker (são responsáveis por processar as requisições de forma eficiente). Eles podem atuar como proxy reverso, buscar arquivos locais, ou até mesmo acionar scripts, como PHP. A quantidade de workers se ajusta ao número de núcleos do servidor.
  
  •	pcre_jit on: Ativa um módulo que acelera a execução de expressões regulares, garantindo uma performance mais otimizada.
  
  •	error_log /var/log/nginx/error.log warn: Centraliza o log de erros de cada host virtual, facilitando a identificação e resolução de problemas.
  
  •	include /etc/nginx/modules/*.conf: Permite a importação de módulos personalizados, expandindo as funcionalidades do NGINX conforme suas necessidades.
  
  •	events { worker_connections 1024 }: Define o número máximo de conexões que cada worker pode gerenciar enquanto aguarda a resposta do proxy reverso. Pode ser ajustado de acordo com a demanda.
  
  •	http { ... }: Configura o ambiente da aplicação. Alguns detalhes importantes incluem:
  
    o	include /etc/nginx/mime.types: Define como o conteúdo será reconhecido e processado (HTML, CSS, JS).
    
    o	server_tokens off: Desabilita o envio da versão do NGINX nos headers, aumentando a segurança contra-ataques.
    
    o	client_max_body_size 1m: Limita o tamanho máximo dos uploads, protegendo o servidor contra sobrecarga.
    
    o	tcp_nopush on: Otimiza o envio de arquivos ao evitar a fragmentação dos dados.
    
  Cada um desses parâmetros ajuda a garantir que o NGINX funcione da forma mais eficiente e segura possível, oferecendo uma base sólida para qualquer aplicação web.
