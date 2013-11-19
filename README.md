Wordpress Escalável
======================

Este repositório lhe ajudará a subir uma instalação do Wordpress com escalabilidade automática. O Memcached cuidará do
Cache das paginas e os uploads serão feitos no AWS S3.

Para o correto funcionamento do Wordpress os plugins a seguir já estão instalados e devem ser ativados:

Batcache - http://wordpress.org/plugins/batcache/
Memcachier - http://wordpress.org/plugins/memcachier/
Amazon S3 and Cloudfront - http://wordpress.org/plugins/amazon-s3-and-cloudfront/


Criando a aplicação
----------------------------

Crie sua conta em http://getupcloud.com/ e instale o RHC (https://getup.zendesk.com/entries/23056511)

Crie uma aplicação php-5.3 (você pode escolher o nome que bem entender)

    rhc app create wordpress php-5.3 mysql-5.1 http://reflector-getupcloud.getup.io/reflect?github=getupcloud/openshift-origin-cartridge-memcached --from-code=https://github.com/getupcloud/wordpress-escalavel.git -s

Agora acesse a url da sua aplicação:

    http://wordpress-$namespace.getup.io
    
Você precisará preencher os dados solicitados para concluir a instalação.


Configurando o Wordpress:
----------------------------

Assim que acessar o painel administrativo, ative os plugins Batcache, Amazon Web Services Amazon S3 and Cloudfront.

Nota: Para que seja possível escalar o Wordpress as imagens e vídeos da galeria devem ser armazenados no S3. Se você já tem uma bucket no S3 basta configurar o plugin informando as credenciais. Se você ainda não tem entre em contato com a Getup suporte@getupcloud.com


Nota
=====

GIT_ROOT/.openshift/action_hooks/deploy:
    
    Este script é executado a cada 'git push'.  Sinta-se à vontade para modifica-lo e
    tirar melhor proveito. Por default este script popula o banco de dados
    do wordpress

    Se você quiser alterar o schema, bata criar um arquivo em:
    GIT_ROOT/.openshift/action_hooks/alter.sql e utilizar o script
    GIT_ROOT/.openshift/action_hooks/deploy para executar a importação do banco,
    não se esqueça de fazer um backup da aplicação e do banco: 'rhc app snapshot save'

Segurança
-----------------------
Consulte a documentação oficial do Wordpress e procure as melhores práticas de segurança. O OpenShift 
gera automaticamente a chaves de instalação em wp-config.php, sinta-se à vontade para alterar.
