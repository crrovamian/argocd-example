# argocd-example

## Instalación de ArgoCD

### 1. Crear namespace para ArgoCD

```bash
kubectl create namespace argocd
```

### 2. Instalar ArgoCD

```bash
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

### 3. Obtener la contraseña inicial

La contraseña por defecto es el nombre del servidor (admin).

```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

### 4. Acceder a la UI

#### Puerto local con kubectl port-forward

```bash
kubectl port-forward -n argocd svc/argocd-server 8080:443
```

Acceder a: http://localhost:8080

Usuario: `admin`
Contraseña: (la obtenida en el paso 3)

#### Alternativa: Cambiar contraseña

```bash
argocd login localhost:8080
argocd account update-password
```