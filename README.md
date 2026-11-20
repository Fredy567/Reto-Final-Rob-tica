# RC-1 — Control PID: del simulador al robot real

Proyecto CapyTown · Robótica (08079) · Universidad ESAN · 2026-2 · Robot MicroROS-Pi5 (Yahboom)

## Integrantes

| Integrante | Partes del RC-1 | Rol (RC-0) |
|---|---|---|
| Fredy Alonso Toribio Sotelo | A (simulador), B (Experimento 1: recta), F (evidencia y comparación) | _completar_ |
| Madeline Trisha Chavez Cervantes | C (Experimento 2: giro de 90°) | _completar_ |
| Nilser Maier Villalobos Sernaque | D (Experimento 3: cuadrado de 2 × 2 m) | _completar_ |
| Walter Alexander Yucra Leyva | E (robot real) | _completar_ |

## Configuración

- **ROS_DOMAIN_ID:** 20
- **Simulador:** `yahboomcar_sim`, `world:=arena_rc1`, `start:=1.0,1.0,0.0`, `robot_radius:=0.14`
- **Nivel de ruido:** `noise:=high` en la Parte A, `noise:=low` en las Partes B–D (valor de trabajo) y `noise:=medium` en una corrida por prueba de la Parte D (prueba de estrés).
- **Robot real:** bringup `capytown_esan`, contenedor Docker `ros2_dev`. `/odom` lo publica `odom_corrector` (calibración del RC-0: r = 0.0325 m, b_eff = 0.24 m) a ~11 Hz. No hay EKF.
- **Sesión del 19/11 (3A con cinta):** se lanzó `yahboomcar_bringup`, que publicó un `/odom` defectuoso (no registraba giros). Esas corridas se reportan solo con cinta; ver `csv/hoja_resultados.csv`.

## Ganancias finales

Detalle completo en `config/rc1_pid.yaml`.

| Prueba | Simulador | Robot real |
|---|---|---|
| Recta 1D | kp 3.0 · ki 0.5 · kd 4.0 | kp 2.4 · ki 0.20 · kd 0.30 (v 0.10) |
| Giro 90° | kp_yaw 6.0 · ki_yaw 0.0 · kd_yaw 0.6 | kp_yaw 6.0 · ki_yaw 0.0 · kd_yaw 0.6 |
| Cuadrado 3B | kp 3.0 · ki 0.0 · kd 4.0 · kp_yaw 3.0 · kd_yaw 0.4 | kp 1.8 · ki 0.10 · kd 1.5 · kp_yaw 2.0 · ki_yaw 0.0 · kd_yaw 0.6 |

## Estructura

```
config/rc1_pid.yaml        ganancias finales (bloques simulador y robot real)
csv/                       un CSV por prueba + hoja_resultados.csv + tabla_transferencia.csv
plots/                     un PNG por prueba (09_plot_csv / cierre_real)
bags/                      bags del cuadrado en el robot real
sim_log.txt, rqt_graph.png Parte A
informe.pdf                informe de 1 página
```

Convención de nombres: `*_sim` = simulador (según /odom), `*_simreal` = simulador (pose real de `cierre_real.py`), `*_real` = robot real.

## Entrega

```
git add .
git commit -m "RC-1: entrega final"
git tag v1.0-rc1
git push origin main --tags
```
