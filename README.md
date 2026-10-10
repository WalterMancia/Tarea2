# Modelo de Amenazas: E-Commerce Platform

Modelo de amenazas de una plataforma de comercio electrónico, elaborado con **OWASP Threat Dragon** y el método **STRIDE**.

- **Curso:** Seguridad en Aplicaciones
- **Programa:** Maestría en Seguridad Informática, Universidad Mariano Gálvez de Guatemala
- **Autor:** Walter Mancia 1793-18-7411
- **Revisor:** CESAR GIOVANNI RODRIGUEZ MINAS
- **Aplicación evaluada:** E-Commerce Platform (React, Node.js/Express, MySQL, Stripe, Cloudinary)

## Contenido del repositorio

| Archivo | Descripción |
|---|---|
| `Informe_Modelo_de_Amenazas.pdf` | Informe completo: alcance, arquitectura, DFD, STRIDE, riesgos, casos de abuso, controles, matriz de remediación y roadmap |
| `modelo-amenazas-ecommerce.json` | Modelo de OWASP Threat Dragon (fuente oficial del modelo) |
| `DFD_Nivel0.png` | DFD Nivel 0: contexto general |
| `DFD_Nivel1.png` | DFD Nivel 1: procesos, almacenes de datos, flujos y límites de confianza |
| `DFD_Nivel2.png` | DFD Nivel 2: checkout y pago |
| `Reporte_Threat_Dragon.pdf` | Reporte de amenazas generado por la herramienta |
| `README.md` | Este documento |

## Cómo abrir el modelo

1. Abre OWASP Threat Dragon (aplicación de escritorio o versión web).
2. Elige la opción de abrir un modelo existente y selecciona `modelo-amenazas-ecommerce.json`.
3. En la sección **Diagrams** del resumen encontrarás los tres diagramas.

## Resumen del modelo

**Diagramas:** 3 (Nivel 0, 1 y 2). **Límites de confianza:** 4.

| ID | Límite de confianza | Qué separa |
|---|---|---|
| TB1 | Navegador del usuario | Cliente no confiable y servidor |
| TB2 | Host Docker | Internet y servidor (puertos 80, 3000 y 3306) |
| TB3 | Zona de datos | API y base de datos |
| TB4 | Terceros SaaS | Plataforma, Stripe y Cloudinary |

**Amenazas identificadas:** 23 (3 críticas, 10 altas, 8 medias y 2 bajas), clasificadas con impacto × probabilidad.

| Nivel | Cantidad | IDs |
|---|---|---|
| Crítico | 3 | T01, T02, T05 |
| Alto | 10 | T03, T04, T06, T07, T11, T12, T18, T19, T22, T23 |
| Medio | 8 | T08, T09, T10, T13, T14, T15, T16, T20 |
| Bajo | 2 | T17, T21 |

> En Threat Dragon la severidad solo admite Baja, Media y Alta. Por eso "Crítico" y "Alto" aparecen como *High*, y el nivel real figura entre corchetes en el título de cada amenaza (por ejemplo, `T01 [Crítico]`).

### Top 10 de hallazgos prioritarios

1. **T01:** Sin rate limiting en autenticación.
2. **T02:** Cantidades negativas o sin validar en carrito y checkout.
3. **T05:** Tráfico sin TLS.
4. **T23:** Cuenta de administrador sin MFA.
5. **T12:** MySQL expuesto y uso del usuario root.
6. **T04:** Refresh token sin rotación ni revocación.
7. **T03:** Tokens en localStorage sin CSP.
8. **T06:** Condición de carrera en el stock del checkout.
9. **T07:** Stock retenido por órdenes sin pagar.
10. **T19:** Sin validación de entrada en autenticación.

## Metodología

1. Levantamiento de arquitectura: inventario de componentes y activos a partir del código fuente.
2. Construcción de DFD en tres niveles con OWASP Threat Dragon.
3. Análisis de amenazas con STRIDE sobre procesos, almacenes de datos y flujos.
4. Priorización con matriz de impacto × probabilidad (Crítico: puntaje ≥ 9, Alto: 5 a 8, Medio: 3 a 4, Bajo: ≤ 2).
5. Casos de abuso para las amenazas críticas y altas.
6. Definición de controles, plan de remediación y roadmap a 12 meses.

**Alcance y limitaciones:** el análisis se basó en una revisión estática del código fuente. No se realizaron pruebas dinámicas de penetración.

## Versionado del modelo

El archivo `.json` es el artefacto oficial del modelo y se mantiene bajo control de versiones. Cada cambio de arquitectura o de amenazas debe ir en un commit con mensaje descriptivo, y el modelo debe revisarse antes de cada release (SSDLC).

| Versión | Fecha | Cambios |
|---|---|---|
| 1.0 | [09-10-2026] | Modelo inicial: 3 DFD, 4 límites de confianza y 23 amenazas STRIDE |

## Licencia y uso

Material académico elaborado para el curso de Seguridad en Aplicaciones. Las amenazas descritas corresponden a una aplicación de práctica y no a un sistema en producción.
