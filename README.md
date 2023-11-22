# Phishing com Kali Linux/setoolkit e apache2 HTTP server

## Configurações:
Antes de iniciar o setoolkit, precisamos realizar algumas configurações para utilizá-lo com o apache2. Por default, as configurações do setoolkit ficam no arquivo set.config no path -> /etc/setoolkit/set.config/ .

![imagem 8](images/8.png "imagem")

---

### Vamos abrir o arquivo com um editor de texto e editar as linhas sublinhadas nas imagens a seguir, deixando da forma como estão exibidas neste exemplo:

![imagem 9](images/9.png "imagem")

![imagem 10](images/10.png "imagem")

![imagem 11](images/11.png "imagem")

**OBS:** *Caso você tenha definido outro diretório raiz para o Apache que não seja o padrão, acrescente esse path no lugar do caminho /var/www/html/ .*

### Porque utilizar o apache2 ?

Como informado no arquivo de configuração do próprio setoolkit, a utilização do apache2 aumenta a performance do vetor de ataque quando utilizado no lugar do web server default, que é o Python Web Server.

![imagem 12](images/12.png "imagem")

# Vamos começar!

## Passo 1:

Com as configurações previamente realizadas, abra seu terminal como root e execute o seguinte comando:

```zsh
$ setoolkit
```
Selecione a primeira opção na tela que será exibida, "Social-Engineering Attacks".

![imagem 1](images/1.png "imagem")

## Passo 2:

Selecione a segunda opção, "Website Attack Vectors".

![imagem 2](images/2.png "imagem")

## Passo 3:

Selecione a terceira opção, "Credential Harvester Attack Method".

![imagem 3](images/3.png "imagem")

## Passo 4:

Selecione a segunda opção, "Site Cloner".

![imagem 4](images/4.png "imagem")

Essa opção nos permite criar uma fakepage estática, clonando uma página de formulário POST qualquer e rodando em um servidor particular. Caso a pessoa preencha os dados do formulário falso, vamos receber os valores e redirecionar a pessoa para a página original na qual ela estava tentando acessar (página clonada).

## Passo 5:

Nesta etapa, é preciso informar o IP hospedeiro da página fake e o site a ser clonado via protocolo HTTP. O setoolkit já sugere o ip do host no momento da seleção da ferramenta Site Cloner. Basta pressionar Enter caso queira utilizar o IP sugerido ou adicionar outro de sua preferência *(Atenção para manter as mesmas configurações no apache2. As portas também precisam ser as mesmas no apache2 e no setoolkit, que escutam na porta 80 por default)*. Em seguida, é preciso inserir a URL do site que será clonado via HTTP. O processo pode demorar alguns minutos.

![imagem 5](images/5.png "imagem")

## Passo 6:

Após o fim do processo, é possível que o terminal nos informe que o service do apache2 pode não estar rodando e se queremos que o setoolkit o inicie para nós. Vamos confirmar com a letra y.

![imagem 14](images/14.png "imagem")

## Onde os logs serão salvos?

Logo após a cópia do site ter sido concluída, somos informados que o serviço já está no ar e que os logs serão salvos no diretório raiz do apache, sob o nome de harvester seguido das informações da data e no formato .txt.

![imagem 15](images/15.png "imagem")

## Acessando a página clonada:

Agora, ao inserirmos o IP na barra de endereços do navegador, será exibida uma versão falsa da página clonada. Depois de preecher o formulário e submeter, a pessoa será redirecionada ao site original e poderemos ter acesso aos dados inseridos no formulário.    

![imagem 6](images/6.png "imagem")

![imagem 6-1](images/6-1.png "imagem")

## Resultado:

Pronto! Se tudo deu certo, os valores inseridos no formulário estarão contidos no local informado pelo setoolkit, que é o diretório raiz do apache2, no caso deste exemplo, /var/www/html .

Abrindo o terminal e nos movendo para o diretório, podemos ver o arquivo harvester_DATADEUSO.txt

![imagem 16](images/16.png "imagem")

---

Utilizando o comando ```cat``` para exibir o conteúdo do arquivo ou simplesmente abrindo com um editor de texto, podemos ver o registro dos valores inseridos pela pessoa no formulário.

![imagem 17](images/17.png "imagem")

---

# *Utilize os aprendizados com sabedoria!*