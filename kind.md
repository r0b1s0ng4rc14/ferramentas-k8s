#Kind

Kind é uma ferramenta para executar clusters Kubernetes locais usando "nós" de contêiners do Docker.

Documentação [kind](https://kind.sigs.k8s.io/docs/user/quick-start/)

Para fazer a instalação no Linux, execute os seguintes comandos.
```
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.8.1/kind-$(uname)-amd64
```

```
chmod +x ./kind
```

```
mv ./kind /usr/bin/kind
```

## Criando um cluster com kind

```
kind create cluster
```

O processo para criação levou 2 minutos
```
kind create cluster
Creating cluster "kind" ...
 ✓ Ensuring node image (kindest/node:v1.18.2) 🖼 
 ✓ Preparing nodes 📦  
 ✓ Writing configuration 📜 
 ✓ Starting control-plane 🕹️ 
 ✓ Installing CNI 🔌 
 ✓ Installing StorageClass 💾 
Set kubectl context to "kind-kind"
You can now use your cluster with:

kubectl cluster-info --context kind-kind

Not sure what to do next? 😅  Check out https://kind.sigs.k8s.io/docs/user/quick-start/
```

Vamos criar outro cluster
```
kind create cluster --name vader
kind create cluster --name vader
Creating cluster "vader" ...
 ✓ Ensuring node image (kindest/node:v1.18.2) 🖼
 ✓ Preparing nodes 📦  
 ✓ Writing configuration 📜 
 ✓ Starting control-plane 🕹️ 
 ✓ Installing CNI 🔌 
 ✓ Installing StorageClass 💾 
Set kubectl context to "kind-vader"
You can now use your cluster with:

kubectl cluster-info --context kind-vader
```

Usando ferramenta kubectx para mostrar os contextos

```
kubectx
  kind-kind
* kind-vader 
```

Usando ferramenta kubens para mostrar os namespaces

```
kubens
* default
  kube-node-lease
  kube-public
  kube-system
  local-path-storage

```
Verificando os cluster via kind:
```
kind get clusters
kind
vader
```
Listando estruta que o kind criou no docker:

```
docker ps
CONTAINER ID        IMAGE                  COMMAND                  CREATED             STATUS              PORTS                       NAMES
99604c72d28f        kindest/node:v1.18.2   "/usr/local/bin/entr…"   14 minutes ago      Up 14 minutes       127.0.0.1:33367->6443/tcp   vader-control-plane
be4368425cf5        kindest/node:v1.18.2   "/usr/local/bin/entr…"   17 minutes ago      Up 17 minutes       127.0.0.1:38985->6443/tcp   kind-control-plane

```
kind delete cluster
kind delete cluster --name vader
Destruindo os cluster:
```


# Instação do docker 

Documentação [docker](https://docs.docker.com/engine/install/)

## Instalação

```
 curl -fsSL https://get.docker.com | bash
```