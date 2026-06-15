# Sports Performance Intelligence

Analizador de rendimiento deportivo (Baloncesto NBA, temporada 2025-26, 8 equipos).
Proyecto de Programación IA - Recuperación Junio 2026.

## 1. Instalación

Requiere Python 3.10+.

```bash
cd sports_performance_intelligence
python -m venv venv
source venv/bin/activate        # En Windows: venv\Scripts\activate
pip install -r requirements.txt
```

## 2. Estructura del proyecto

```
sports_performance_intelligence/
├── data/
│   ├── raw/          -> datos originales (Basketball-Reference, filtrados)
│   └── processed/    -> CSV finales + sports.db (generados por el pipeline)
├── src/               -> codigo fuente (ETL, metricas, analisis, ML...)
├── dashboard/         -> paginas del dashboard Streamlit
├── reports/           -> informes/exportaciones generadas
├── notebooks/         -> notebooks de exploracion
├── app.py             -> punto de entrada del dashboard
├── requirements.txt
└── README.md
```

## 3. Ejecutar el pipeline de datos

Genera/regenera los ficheros de `data/processed/` a partir de `data/raw/`:

```bash
cd notebooks
python build_players_teams.py     # -> teams.csv, players.csv
python generate_matches.py        # -> matches.csv, player_game_stats.csv
cd ..
cd src
python metrics.py                 # -> players_with_metrics.csv
python analysis.py                # demo: rankings, comparativas, anomalias (opcional)
python clustering.py              # -> players_clustered.csv
```

Cada script imprime un resumen por pantalla (filas generadas, comprobaciones,
ejemplos) para verificar que todo ha funcionado correctamente.

## 4. Lanzar el dashboard

```bash
cd sports_performance_intelligence   # raiz del proyecto (NO entrar en src/)
streamlit run app.py
```

Se abrira en el navegador (http://localhost:8501) con 6 pestanas:
Rankings, Comparativas, Evolucion temporal, Distribucion de eventos,
Clustering y Patrones/anomalias. Filtros de equipo/rol/min. partidos en la
barra lateral.
