
# GitFlow Demo

Este repositorio muestra un caso práctico completo de GitFlow, desde la creación del repositorio hasta la implementación de un flujo automatizado con GitHub Actions. Los participantes podrán seguir los pasos copiando y pegando los comandos en su terminal para aprender y practicar.

---

## **Requisitos Previos**
1. Tener instalado `git` y `git-flow`:
   - **Ubuntu/Debian**: `sudo apt install git git-flow`
   - **MacOS**: `brew install git-flow`
2. Tener una cuenta en [GitHub](https://github.com/).
3. Un editor de texto como Visual Studio Code o cualquier IDE de tu preferencia.

---

## **1. Configuración Inicial**

### Clonar el repositorio
Clona este repositorio en tu máquina local:
```bash
git clone https://github.com/<tu_usuario>/gitflow-demo.git
cd gitflow-demo
```

### Inicializar GitFlow
Inicializa GitFlow en el repositorio:
```bash
git flow init
```
Acepta las configuraciones predeterminadas:
- **master**: Producción.
- **develop**: Desarrollo.

Crea un archivo inicial para el proyecto:
```bash
echo "# GitFlow Demo" > README.md
git add README.md
git commit -m "docs: initialize repository with README"
git push -u origin master
git push -u origin develop
```

---

## **2. Ciclo de Vida de un Cambio**

### **Ambiente: DEV**
1. Crea una rama `feature` para desarrollar una nueva funcionalidad:
   ```bash
   git flow feature start add-login-page
   ```

2. Crea un archivo básico `login.html`:
   ```bash
 __________________________________________  
   echo "<!DOCTYPE html>
<html>
<head>
    <title>Login Page</title>
</head>
<body>
    <h1>Welcome to the Login Page</h1>
    <form>
        <label for='username'>Username:</label>
        <input type='text' id='username' name='username'><br><br>
        <label for='password'>Password:</label>
        <input type='password' id='password' name='password'><br><br>
        <button type='submit'>Login</button>
    </form>
</body>
</html>" > login.html

__________________________________________________________
   ```

3. Agrega y confirma los cambios:
   ```bash
   git add login.html
   git commit -m "feat: add basic login page"
   ```

4. Mejora el diseño con estilos básicos:
   ```bash
   echo "<style>
body { font-family: Arial, sans-serif; margin: 20px; }
form { border: 1px solid #ccc; padding: 15px; width: 300px; }
</style>" >> login.html
   git add login.html
   git commit -m "style: add basic styles for login page"
   ```

5. Finaliza la rama `feature` y fusiónala en `develop`:
   ```bash
   git flow feature finish add-login-page
   git push origin develop
   ```

---

### **Ambiente: QA**
1. Crea una rama `release` para preparar un lanzamiento:
   ```bash
   git flow release start v1.0.0
   ```

2. Prepara el archivo para producción:
   ```bash
   echo "<footer>Version 1.0.0</footer>" >> login.html
   git add login.html
   git commit -m "chore: prepare release v1.0.0"
   ```

3. Finaliza la rama `release`:
   ```bash
   git flow release finish v1.0.0
   git push origin master
   git push origin develop
   git push --tags
   ```

---

### **Ambiente: UAT**
1. Crea una rama `hotfix` para corregir errores:
   ```bash
   git flow hotfix start fix-login-bug
   ```

2. Realiza una corrección en el archivo:
   ```bash
   echo "<!-- Fixed typo in form labels -->" >> login.html
   git add login.html
   git commit -m "fix: correct typo in login page form"
   ```

3. Finaliza la rama `hotfix`:
   ```bash
   git flow hotfix finish fix-login-bug
   git push origin master
   git push origin develop
   git push --tags
   ```

---

## **3. Automatización con GitHub Actions**

1. Crea el archivo de flujo en `.github/workflows/ci.yml`:
   ```bash
   mkdir -p .github/workflows
   echo "
   name: CI/CD Pipeline

   on:
     push:
       branches:
         - develop

   jobs:
     build:
       runs-on: ubuntu-latest

       steps:
       - name: Checkout code
         uses: actions/checkout@v2

       - name: Set up Docker
         uses: docker/setup-buildx-action@v2

       - name: Build Docker image
         run: |
           docker build -t gitflow-demo:latest .

       - name: Run tests
         run: |
           echo 'No tests configured yet'
   " > .github/workflows/ci.yml
   ```

2. Agrega y confirma los cambios:
   ```bash
   git add .github/workflows/ci.yml
   git commit -m "ci: add GitHub Actions workflow for Docker build"
   git push origin develop
   ```

---

## **4. Verificar el Flujo**
1. Revisa el historial de ramas (`feature`, `release`, `hotfix`).
2. Valida los pipelines en la pestaña **Actions** del repositorio en GitHub.

---

## **5. Extensiones posibles**
- Añadir pruebas unitarias.
- Implementar despliegues automáticos con GitHub Actions.

---

¡Sigue estos pasos y explora GitFlow! Si tienes preguntas, abre un issue en este repositorio.

Conectemos:

www.linkedin.com/in/miguelsancor
