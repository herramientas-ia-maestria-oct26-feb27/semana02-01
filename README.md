# Semana 2 · Herramientas para Inteligencia Artificial


## Organización


1. `Ejemplo-01-Pandas.ipynb` — lectura, selección, filtrado, nulos y agrupaciones.
2. `Ejemplo-02-Pandas-Polars.ipynb` — mismas operaciones, `scan_csv` y tiempos.
3. `Ejemplo-03-Scikit-Learn.ipynb` — clasificación, entrenamiento y evaluación.
4. `Ejemplo-04-NLTK.ipynb` — tokenización y frecuencia de palabras.
5. `Ejemplo-05-spaCy.ipynb` — tokenización y modelo lingüístico opcional.
6. `Ejemplo-06-Matplotlib.ipynb` — histogramas, barras y dispersión.

Los archivos `data/rendimiento_100.csv`, `data/rendimiento_1000.csv` y `data/rendimiento_10000.csv` son **datos sintéticos anidados**: las primeras 100 filas son idénticas en los tres archivos. Se generaron relaciones artificiales entre horas, asistencia y notas para demostrar análisis y clasificación. Los comentarios son plantillas ficticias; **no** representan opiniones auténticas. La nota faltante implica `aprobado` faltante. El umbral de aprobación es 70/100, no una norma institucional.

## Entornos virtuales fuera de la carpeta del proyecto

Se recomienda Python **>3.11**.

### Linux / macOS

Desde la carpeta que contiene `Semana_02_Herramientas_IA`, por ejemplo:

```bash
python3.11 -m venv entornos/semana02
source entornos/semana02/bin/activate
cd Semana_02_Herramientas_IA
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
jupyter lab
```

También puede crear el entorno con `virtualenv -p python3.11 entornos/semana02`.

### Windows PowerShell

Desde la carpeta padre del proyecto:

```powershell
py -3.11 -m venv entornos\semana02
.\entornos\semana02\Scripts\Activate.ps1
cd Semana_02_Herramientas_IA
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
jupyter lab
```

### Windows CMD

```bat
py -3.11 -m venv entornos\semana02
entornos\semana02\Scripts\activate.bat
cd Semana_02_Herramientas_IA
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
jupyter lab
```

Si PowerShell bloquea la activación, utilice CMD o revise la política de ejecución de scripts de su equipo.
