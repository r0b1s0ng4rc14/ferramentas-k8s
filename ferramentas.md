#Dicas de ferramentas para Administrar Kubernetes


#Kubectl

##Objetivo
A ferramenta permite executar comandos em clusters, implantar, inspecionar e gerenciar recursos [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

##Instalação

```
 curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
```

```
chmod +x ./kubectl
```

```
sudo mv ./kubectl /usr/bin/kubectl
```
##Incluindo o auto-completar

Pacote necessário: (bash-completion)
```
sudo apt-get install bash-completion
```
##Adicionando auto completar para seu usuario
```
echo 'source <(kubectl completion bash)' >>~/.bashrc
```

#Stern

##Objetivo
Acompanhar e análisar vários pods e containers no Kubernetes. Cada resultado é codificado por cores para uma depuração mais rápida. 

##Instalação
Repositório  [Github](https://github.com/wercker/stern)

Baixe o arquivo [stern-versão-1.11.0](https://github.com/wercker/stern/releases/download/1.11.0/stern_linux_amd64)
**Obs: O legal é sempre baixar a última versão estável.**

Agora é necessário dar permissão de execução:
```
chmod +x ~/Downloads/stern_linux_amd64
```

Mova para pasta de binários
```
sudo mv ~/Downloads/stern_linux_amd64 /usr/bin/stern
```
Está pronto para uso.

##Exemplos de uso

Se eu tenho dois containers rodando dentro do pod observer, para pegar os logs de ambos eu executo:

```
kubectl logs -f -n kube-system observer --all-containers
```

Os logs aparecem sem destaques de cores e fica um pouco difícil de ler dependendo do volume de logs.

Rodando o mesmo exemplo com o Stern:
```
stern -n kube-system observer
```
Os logs vão aparecer com o visual diferenciado, separando em cores isso ajuda em um trobleshooting.

Outra opção legal é adicionar filtro com base no tempo, exemplo abaixo aplica nos últimos 30 minutos.:
```
stern -n kube-system observer -t --since 30m
```

# Kubectx & Kubens

**Estas ferramentas tem depência direta do kubectl**

##Objetivo
O Kubectx é uma ferramenta para gerenciar e alternar entre seus contextos.

#Kubens
O Kubens é uma ferramenta para alternar entre suas namespaces, no contexto atual setado.

##Instalação

###Kubectx
[Github](https://github.com/ahmetb/kubectx)

Baixe o arquivo [kubectx](https://github.com/ahmetb/kubectx/releases/download/v0.9.1/kubectx)
**Obs: O legal é sempre baixar a última versão estável.**

Agora é necessário dar permissão de execução:
```
chmod +x ~/Downloads/kubectx
```

Mova para pasta de binários
```
sudo mv ~/Downloads/kubectx /usr/bin/kubectx
```
##Exemplos de uso
```
USAGE:
  kubectx                   : list the contexts
  kubectx <NAME>            : switch to context <NAME>
  kubectx -                 : switch to the previous context
  kubectx -c, --current     : show the current context name
  kubectx <NEW_NAME>=<NAME> : rename context <NAME> to <NEW_NAME>
  kubectx <NEW_NAME>=.      : rename current-context to <NEW_NAME>
  kubectx -d <NAME>         : delete context <NAME> ('.' for current-context)
                              (this command won't delete the user/cluster entry
                              that is used by the context)
  kubectx -u, --unset       : unset the current context
``` 

###Kubens

Baixe o arquivo [kubens](https://github.com/ahmetb/kubectx/releases/download/v0.9.1/kubens)
**Obs: O legal é sempre baixar a última versão estável.**

Agora é necessário dar permissão de execução:
```
chmod +x ~/Downloads/kubens
```

Mova para pasta de binários
```
sudo mv ~/Downloads/kubens /usr/bin/kubens
```

Está pronto para uso.

##Exemplos de uso
```
USAGE:
  kubens                    : list the namespaces
  kubens <NAME>             : change the active namespace
  kubens -                  : switch to the previous namespace
  kubens -c, --current      : show the current namespace
```
