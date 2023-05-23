# SSH Keys Github

> Adicionando chave SSH para transferir conteúdo do projeto dentro de um repositórios local para o repositório remoto no Github.

## 🗝 Gerando a chave 

Primeiramente, devemos gerar um novo par de chaves usando o comando ssh-keygen:
```
ssh-keygen -t rsa -b 4096 -C "seu-email@seu-servidor.com"
```

O comando irá perguntar em qual arquivo você deseja salvar sua chave.

Se você não tem nenhuma chave configurada, não tem problema usar o nome padrão (id_rsa), pra isso apenas aperte `Enter` e ela será criada no caminho indicado entre parênteses.

Em seguida, ele perguntará se você deseja usar uma senha.
Se criar a senha, ela será solicitada todas as vezes que você fizer uma autenticação baseada nas suas chaves.

Apenas é recomendado configurar uma senha se você compartilha o computador com outras pessoas.
```
Enter passphrase (empty for no passphrase): [digite sua senha] //Aperte enter caso não queria add password.
Enter same passphrase again: [digite sua senha novamente] //Aperte enter caso não tenha criado password.
```

Finalmente, sua chave será salva na pasta informada anteriormente:
```
Your identification has been saved in /Users/wolner/.ssh/id_rsa.
Your public key has been saved in /Users/wolner/.ssh/id_rsa.pub.
The key fingerprint is:
01:0f:f4:3b:ca:85:d6:17:a1:7d:f0:68:9d:f0:a2:db seu-email@seu-servidor.com
```

## 🔐 Adicionando a chave no Github

Acesse o caminho que foi gerada a cahve e encontrará dois arquivos. O de extensão `.pub` é o que contém a chave pública que iremos utilizar. 

No interior do arquivo, seleciona e copie a chave que começa com `ssh-rsa` seguida de uma cadeira de caracteres.

No Github, acess `Configurações`, no menu lateral esquerdo clique em `SSH and GPS keys` e clique no botão `Add SSH key`. 

Haverá um campo de título (opcional) e o campo da chave, onde deverá ser colada a chave pública que foi gerada.

Clique em `Add SSH key` e confirme a operação inserindo a senha do Github.

## 🧨 Desvincular repositório remoto

Caso o repositório local ja esteja vinculado a algum repositorio remoto, será preciso desvincular de modo a permitir a continuidade dos passos abaixo. Em caso negativo, pode-se pular desta etapa para a proxima.
```
git remote rm origin //Remover o repositório remoto vinculado.
git remote //consulta se foi mesmo removido
```

## ✨ Associar repositório remoto
```
git init
git remote add origin git@github.com:"usuario/repositorio-aqui".git
```

Agora deve-se atentar se o repositório remoto ja cont´rm algum arquivo (como o README, por exemplo), pois isto irá definir qual dos dois passos seguinte será utilizado.

## 📭 Sem arquivos/README:
```
git push -u origin master
```

## 📬 Com arquivos/READEME:
```
git add .
git commit -m"comentário"
//Tratar de resolver conclito aqui no meio!!
git pull origin master --allow-unrelated-histories
git push -u origin master
```
