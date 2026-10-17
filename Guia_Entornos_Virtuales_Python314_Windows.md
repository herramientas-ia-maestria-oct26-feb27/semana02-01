# Guía práctica: entornos virtuales de Python 3.14 en Windows

**Sistema operativo:** Windows 10 u 11  
**Consolas:** Símbolo del sistema (**CMD**) y **PowerShell**  
**Requisito previo:** Python **3.14** instalado y funcionando correctamente.

## 1. ¿Qué es un entorno virtual?

Un **entorno virtual** es un espacio aislado donde se instalan las bibliotecas de Python que necesita una actividad o proyecto. De esta forma, las dependencias de una práctica no interfieren con las de otra.

En esta guía se utiliza `venv`, que viene incluido con Python. **El entorno estará fuera de la carpeta del proyecto**, en una carpeta hermana llamada `entornos`.

### Organización recomendada

```text
Documentos\
└── clases-python\
    ├── entornos\
    │   └── entorno-semana02\     ← entorno virtual
    └── semana02\                ← proyecto y notebooks
        ├── requirements.txt
        ├── Ejemplo-01-Pandas.ipynb
        └── data\
```

> **Importante:** No cree el entorno virtual dentro de `semana02`. No copie ni suba el entorno a GitHub; puede recrearse a partir de `requirements.txt`.

## 2. Verificar la versión de Python

Abra **CMD** o **PowerShell** y ejecute:

```bat
py -3.14 --version
o
python --version
```

Debería aparecer una salida similar a `Python 3.14.x`.

> En esta guía utilizamos `py -3.14` para seleccionar explícitamente Python 3.14. Si su equipo no tiene disponible el comando `py`, aunque Python esté instalado, puede usar `python` en los comandos de creación y comprobar previamente `python --version`.

## 3. Crear las carpetas de trabajo

### Opción A: CMD

```bat
cd /d "%USERPROFILE%\Documents"
mkdir clases-python
cd clases-python
mkdir entornos
mkdir semana02
```

Si alguna carpeta existe, Windows puede mostrar un mensaje indicando que ya existe; puede continuar.

### Opción B: PowerShell

```powershell
Set-Location "$HOME\Documents"
New-Item -ItemType Directory -Force -Path clases-python | Out-Null
Set-Location .\clases-python
New-Item -ItemType Directory -Force -Path entornos, semana02 | Out-Null
```

> Si su carpeta **Documentos** está redirigida a OneDrive u otra ubicación, adapte la ruta a la carpeta donde realmente guarda el proyecto.

> Puede crear la ruta de forma gráfica tradicional, lo importante es no perder la ruta en la que se encuentra

## 4. Crear el entorno virtual con `venv`

**En CMD o PowerShell**, situándose en `clases-python`, ejecute:

```bat
py -3.14 -m venv entornos\entorno-semana02
```

El entorno se crea una sola vez. No es necesario crearlo de nuevo cada vez que se trabaja.

## 5. Activar el entorno virtual

### En CMD

Desde `clases-python`:

```bat
entornos\entorno-semana02\Scripts\activate.bat
```

### En PowerShell

Desde `clases-python`:

```powershell
.\entornos\entorno-semana02\Scripts\Activate.ps1
```

Cuando esté activo, al inicio de la línea de comandos verá algo similar a:

```text
(entorno-semana02) C:\Users\Estudiante\Documents\clases-python>
```

**Si PowerShell bloquea el script de activación**, habilite su ejecución **solo en la sesión actual** y vuelva a activarlo:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\entornos\entorno-semana02\Scripts\Activate.ps1
```

## 6. Instalar bibliotecas dentro del entorno

Con el entorno activado, ingrese a la carpeta del proyecto.

**CMD:**

```bat
cd semana02
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

**PowerShell:**

```powershell
Set-Location .\semana02
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

> Los comandos suponen que el archivo `requirements.txt` ya está en `semana02`. **La compatibilidad de las bibliotecas con Python 3.14 depende de sus versiones**: si alguna instalación falla, consulte el mensaje concreto; el entorno virtual no resuelve por sí solo incompatibilidades de paquetes.

Para comprobar qué intérprete y qué instalador está utilizando:

```bat
python --version
python -m pip --version
```

Para mostrar los paquetes instalados:

```bat
python -m pip list
```

## 7. Iniciar JupyterLab (si está instalado)

Con el entorno activo y desde `semana02`:

```bat
python -m jupyterlab
```

Esto abre JupyterLab en el navegador (o muestra una dirección local para abrirlo). Para detener el servidor, regrese a la consola y presione **Ctrl + C**.

Si necesita instalar JupyterLab:

```bat
python -m pip install jupyterlab ipykernel
```

## 8. Desactivar el entorno virtual

En **CMD y PowerShell** se utiliza el mismo comando:

```bat
deactivate
```

Esto devuelve la consola al entorno de Python habitual. **Desactivar no borra el entorno ni desinstala sus bibliotecas.**

## 9. Volver a utilizar el entorno otro día

No vuelva a ejecutar `venv`. Únicamente abra una consola y actívelo.

**CMD:**

```bat
cd /d "%USERPROFILE%\Documents\clases-python"
entornos\entorno-semana02\Scripts\activate.bat
cd semana02
python -m jupyterlab
```

**PowerShell:**

```powershell
Set-Location "$HOME\Documents\clases-python"
.\entornos\entorno-semana02\Scripts\Activate.ps1
Set-Location .\semana02
python -m jupyterlab
```

## 10. Alternativa: crear el entorno con `virtualenv` (opcional)

`virtualenv` es una herramienta adicional; **no necesita instalarla** si utiliza `venv`.

Instálela con Python 3.14:

```bat
py -3.14 -m pip install virtualenv
```

Cree el entorno en la misma carpeta externa al proyecto (escoja **una sola alternativa**, `venv` o `virtualenv`):

```bat
py -3.14 -m virtualenv entornos\entorno-semana02
```

La activación y desactivación son iguales a las de las secciones 5 y 8.

## 11. Problemas frecuentes

| Situación | Qué revisar |
|---|---|
| `py` no se reconoce | Pruebe `python --version`; utilice `python -m venv ...` si apunta a Python 3.14. |
| PowerShell impide activar | Use `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass` o active con CMD. |
| `ModuleNotFoundError` | Active el entorno correcto e instale el paquete con `python -m pip install nombre-paquete`. |
| Jupyter utiliza otro Python | Compruebe el kernel activo y ejecute `import sys; print(sys.executable)` en una celda. |
| Una biblioteca no se instala | Compruebe que dispone de una versión compatible con Python 3.14. |
| No encuentra `requirements.txt` | Compruebe que está en la carpeta `semana02`, donde se encuentra el archivo. |

## 12. Resumen de comandos

| Acción | CMD | PowerShell |
|---|---|---|
| Crear entorno (desde `clases-python`) | `py -3.14 -m venv entornos\entorno-semana02` | `py -3.14 -m venv entornos\entorno-semana02` |
| Activar | `entornos\entorno-semana02\Scripts\activate.bat` | `.\entornos\entorno-semana02\Scripts\Activate.ps1` |
| Instalar paquetes | `python -m pip install -r requirements.txt` | `python -m pip install -r requirements.txt` |
| Ver paquetes | `python -m pip list` | `python -m pip list` |
| Desactivar | `deactivate` | `deactivate` |

**Actividad de comprobación:** Cree el entorno, actívelo, consulte `python --version`, instale las bibliotecas del proyecto y desactívelo.
