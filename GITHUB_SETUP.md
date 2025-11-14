# 🚀 Instrucciones para Subir a GitHub

Tu repositorio local está completamente preparado en: `/tmp/knapsack-problem-optimization/`

## ✅ Estado Actual del Repositorio

```
✓ Repositorio inicializado con Git
✓ Rama principal: main
✓ 7 archivos preparados:
  ├── README.md (documentación principal)
  ├── LICENSE (MIT)
  ├── requirements.txt (dependencias)
  ├── .gitignore (patrones de Git)
  └── docs/
      ├── ALGORITHMS.md (análisis de algoritmos)
      ├── INSTALL.md (guía de instalación)
      └── RESULTS.md (resultados y recomendaciones)

✓ Primer commit realizado: 79871a7
```

---

## 📋 Pasos para Subir a GitHub

### PASO 1: Crear Repositorio en GitHub

1. Ve a [https://github.com/new](https://github.com/new)
2. Completa el formulario:
   - **Repository name**: `knapsack-problem-optimization`
   - **Description**: `Comparative analysis of exact (CBC) vs greedy algorithms for the 0/1 Knapsack Problem`
   - **Visibility**: Public (para compartir)
   - **Initialize**: NO marques nada (ya tenemos archivos locales)

3. Haz clic en "Create repository"

4. **COPIA la URL** que aparece. Será algo como:
   ```
   https://github.com/TU_USUARIO/knapsack-problem-optimization.git
   ```

---

### PASO 2: Conectar tu Repositorio Local a GitHub

Ejecuta estos comandos en la terminal:

```bash
# Ir al directorio del proyecto
cd /tmp/knapsack-problem-optimization

# Agregar origen remoto (REEMPLAZA TU_USUARIO con tu nombre de usuario de GitHub)
git remote add origin https://github.com/TU_USUARIO/knapsack-problem-optimization.git

# Verificar que se agregó correctamente
git remote -v
```

**Debería mostrar algo como:**
```
origin  https://github.com/TU_USUARIO/knapsack-problem-optimization.git (fetch)
origin  https://github.com/TU_USUARIO/knapsack-problem-optimization.git (push)
```

---

### PASO 3: Subir los Archivos a GitHub

```bash
# Subir la rama main a GitHub
git push -u origin main
```

**Si te pide autenticación:**
- **Opción 1** (Recomendado): Usa GitHub CLI (`gh auth login`)
- **Opción 2**: Genera un Personal Access Token en GitHub Settings → Developer Settings → Personal Access Tokens
- **Opción 3**: Usa SSH en lugar de HTTPS

---

### PASO 4: Verificar en GitHub

1. Ve a `https://github.com/TU_USUARIO/knapsack-problem-optimization`
2. Deberías ver:
   - ✅ Todos tus archivos (README.md, requirements.txt, docs/, etc.)
   - ✅ Un commit mostrando tus cambios
   - ✅ El README renderizado en la página principal

---

## 📝 Comando Rápido (Todos los Pasos)

Si ya tienes configurado Git globalmente con tu email:

```bash
cd /tmp/knapsack-problem-optimization
git remote add origin https://github.com/TU_USUARIO/knapsack-problem-optimization.git
git push -u origin main
```

Listo. Tu repositorio estará en GitHub.

---

## 🎯 Próximos Pasos Opcionales

### 1. Agregar Notebook y Datos

```bash
# Copiar el notebook
cp ~/path/to/mochila.ipynb /tmp/knapsack-problem-optimization/notebooks/

# Copiar datos CSV
cp ~/path/to/datos*.csv /tmp/knapsack-problem-optimization/data/

# Agregar y subir
git add notebooks/ data/
git commit -m "Add notebook and data files"
git push origin main
```

### 2. Agregar GitHub Actions (CI/CD)

Crea un archivo `.github/workflows/tests.yml`:

```yaml
name: Run Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v3
    - uses: actions/setup-python@v4
      with:
        python-version: '3.10'
    
    - name: Install dependencies
      run: |
        pip install -r requirements.txt
    
    - name: Run notebook
      run: |
        jupyter nbconvert --to notebook --execute notebooks/mochila.ipynb
```

### 3. Agregar Badges al README

En la parte superior de `README.md`:

```markdown
# 🎒 Knapsack Problem Optimization

[![GitHub stars](https://img.shields.io/github/stars/TU_USUARIO/knapsack-problem-optimization?style=social)](https://github.com/TU_USUARIO/knapsack-problem-optimization)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![PuLP](https://img.shields.io/badge/PuLP-2.7.0-orange.svg)](https://coin-or.github.io/pulp/)
```

### 4. Crear Release

```bash
# Crear un tag
git tag -a v1.0.0 -m "Version 1.0.0 - Initial Release"

# Subir el tag
git push origin v1.0.0
```

---

## 🔑 Puntos Clave a Recordar

### ⚠️ IMPORTANTE

1. **Reemplaza `TU_USUARIO`** con tu nombre de usuario de GitHub en la URL
2. **Crea el repositorio PRIMERO** en GitHub antes de hacer push
3. **Usa `--initial-branch=main`** para nuevos repositorios (ya hecho)
4. **Verifica la URL remota** con `git remote -v`

### 📊 Verificación Final

```bash
# Ver estado del repositorio
cd /tmp/knapsack-problem-optimization
git status                    # Debe mostrar "working tree clean"
git log --oneline             # Debe mostrar el commit inicial
git remote -v                 # Debe mostrar origin
```

---

## 🆘 Solucionar Problemas

### Error: "fatal: remote origin already exists"

```bash
# Remover el remoto existente
git remote remove origin

# Agregar de nuevo con la URL correcta
git remote add origin https://github.com/TU_USUARIO/knapsack-problem-optimization.git
```

### Error: "Permission denied (publickey)"

Solución: Usar HTTPS en lugar de SSH, o configurar SSH key:
```bash
# Cambiar de SSH a HTTPS
git remote set-url origin https://github.com/TU_USUARIO/knapsack-problem-optimization.git
```

### Error: "Updates were rejected"

```bash
# Si GitHub tiene cambios que no tienes localmente
git pull origin main --allow-unrelated-histories
git push origin main
```

---

## 💡 Consejos

✅ **Hacer commits frecuentes**: Cada cambio importante
✅ **Escribir buenos mensajes**: Describe QUÉ y POR QUÉ
✅ **Usar ramas para features**: `git checkout -b feature/nueva-feature`
✅ **Revisar antes de push**: `git diff` y `git status`
✅ **Mantener actualizado**: `git pull` antes de trabajar

---

## 📚 Recursos Útiles

- [GitHub Docs - Adding a repository](https://docs.github.com/en/repositories/creating-and-managing-repositories)
- [Git Basics - Working with Remotes](https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes)
- [GitHub Help - Setting up your repository](https://help.github.com/categories/setup/)

---

**¡Listo! Tu proyecto está preparado para GitHub.** 🎉

Una vez completes estos pasos, tu repositorio estará visible públicamente en GitHub y podrá ser clonado por cualquiera.

```bash
# Otros podrán clonarlo con:
git clone https://github.com/TU_USUARIO/knapsack-problem-optimization.git
```
