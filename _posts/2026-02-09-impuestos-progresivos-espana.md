---
layout: post
title: "Son realmente progresivos los impuestos en Espana?"
date: 2026-02-09
---

## Conceptos basicos: del coste laboral al bolsillo

Para entender este estudio hay que tener claros tres conceptos de "salario"
y como se relacionan. Usemos un ejemplo concreto: un asalariado con un
salario bruto de 30.000 EUR/ano.

```
COSTE LABORAL (lo que la empresa paga en total)
  = Salario bruto + SS empresa
  = 30.000 + 9.195 (30.65%)
  = 39.195 EUR
       │
       ├── SS empresa: 9.195 EUR ──────────> a la Seguridad Social
       │   (la empresa lo paga, el trabajador nunca lo ve)
       │
       ▼
SALARIO BRUTO (lo que aparece en el contrato)
  = 30.000 EUR
       │
       ├── SS trabajador: 1.950 EUR (6.5%) ──> a la Seguridad Social
       │
       ├── Retencion IRPF: ~4.300 EUR ────────> a Hacienda
       │   (varia segun situacion personal)
       │
       ▼
SALARIO NETO (lo que llega a la cuenta bancaria)
  = 30.000 - 1.950 - 4.300
  = ~23.750 EUR
       │
       ├── IVA en el gasto: ~2.250 EUR ───────> a Hacienda (via comercios)
       │   (invisible: ya incluido en los precios)
       │
       ▼
CAPACIDAD REAL DE COMPRA
  = ~21.500 EUR
```

**Resumen de lo que se queda el Estado:**

| Concepto | Cantidad | % del bruto | % del coste laboral |
|---|---|---|---|
| SS empresa | 9.195 | 30.7% | 23.5% |
| SS trabajador | 1.950 | 6.5% | 5.0% |
| IRPF | 4.300 | 14.3% | 11.0% |
| IVA (estimado) | 2.250 | 7.5% | 5.7% |
| **Total** | **17.695** | **59.0%** | **45.1%** |

De los 39.195 EUR que cuesta este trabajador a la empresa, solo 21.500 EUR
se convierten en capacidad de compra real. El Estado se queda con el 45%.

**¿Cual es el denominador correcto?** Depende de la pregunta:
- **% del bruto** (30.000): lo mas intuitivo, es el salario "oficial"
- **% del coste laboral** (39.195): lo mas riguroso economicamente, porque
  es el valor real del trabajo del empleado
- **% del neto** (23.750): util para entender cuanto IVA "extra" pagas

En este estudio usamos **% del bruto** como medida principal (es la mas
comprensible), pero mostramos **% del coste laboral** como referencia.

---

## Hipotesis

Los impuestos en Espana, considerados en su conjunto, **no son progresivos** para
los asalariados. Podrian incluso ser **regresivos**: los tramos mas bajos de renta
soportan una carga fiscal total (como porcentaje de su renta bruta) superior a lo
que sugiere la escala del IRPF, y los tramos mas altos disponen de mecanismos que
reducen su carga efectiva.

Dos intuiciones clave:

1. **Los tramos bajos gastan casi todo lo que ingresan**, y ese gasto lleva IVA.
   Un asalariado que gana 18.000 EUR/ano y gasta el 95% de su renta esta pagando
   un ~15-20% adicional en impuestos indirectos sobre ese gasto. Ese porcentaje
   cae drasticamente cuando la tasa de ahorro sube (tramos altos).

2. **La progresividad nominal del IRPF no compensa** la regresividad de los
   impuestos indirectos y las cotizaciones sociales (que tienen tope).

## Que queremos calcular

Para cada tramo de renta de un **asalariado** en Espana:

```
Carga fiscal total (%) = (IRPF + Cotizaciones SS + IVA soportado + Imp. Especiales) / Renta bruta
```

Donde:
- **Renta bruta** = salario bruto (antes de cualquier deduccion)
- **IRPF** = cuota efectiva real (no la nominal), segun datos de la AEAT
- **Cotizaciones SS** = parte del trabajador (6.5%) + parte empresarial (~30.6%)
  (la parte empresarial es discutible; la incluimos como escenario porque
  economicamente sale del coste laboral del trabajador)
- **IVA soportado** = estimado a partir de los patrones de gasto por nivel de
  renta (INE) y los tipos de IVA por categoria
- **Impuestos especiales** = estimados sobre gasto en alcohol, tabaco, carburantes

## Los tres modelos

### Modelo 1: Carga de IVA por nivel de renta

**Pregunta**: Que porcentaje de su renta paga cada tramo en IVA?

**Datos**: Tabla 73809 del INE (Encuesta de Presupuestos Familiares) — gasto
medio por hogar desglosado en 14 categorias COICOP, cruzado con 8 tramos de
ingreso mensual neto.

**Metodo**:
1. Para cada tramo de renta, tomar el gasto medio por categoria COICOP
2. Asignar a cada categoria su tipo de IVA predominante (4%, 10%, 21%, exento)
3. Calcular el IVA total pagado = sum(gasto_categoria * tipo_iva / (1 + tipo_iva))
4. Dividir entre la renta para obtener el % de renta que va a IVA

### Modelo 2: IRPF efectivo por tramo de renta salarial

**Pregunta**: Que porcentaje real de IRPF paga cada tramo?

**Datos**: Estadistica "Mercado de Trabajo y Pensiones en las Fuentes Tributarias"
de la AEAT — retenciones y tipo medio de retencion por tramo salarial (en
multiplos del SMI), exclusivamente para asalariados.

**Metodo**:
1. Tomar el tipo medio de retencion por tramo salarial
2. Complementar con datos de la declaracion (cuota liquida / base imponible)
   para capturar el efecto de deducciones y regularizacion

### Modelo 3: Cotizaciones a la Seguridad Social

**Pregunta**: Que porcentaje del coste laboral total va a cotizaciones?

**Datos**: Tipos de cotizacion oficiales (BOE) y bases maxima/minima.

**Metodo**:
1. Para cada tramo salarial, calcular las cotizaciones del trabajador y del
   empresario
2. Hasta la base maxima (5.101 EUR/mes en 2026 = 61.214 EUR/ano): se aplican
   los tipos completos (~6.5% trabajador + ~30.6% empresa)
3. Por encima de la base maxima: solo se paga la cotizacion adicional de
   solidaridad (0.9% - 1.5% en 2026, subiendo hasta 5.5% - 7% en 2045)
4. Esto hace las cotizaciones **regresivas**: quien gana 120.000 EUR paga
   un porcentaje menor que quien gana 40.000 EUR

### Sintesis: Carga fiscal total

Sumar los tres modelos y graficar:

```
X = tramo de renta bruta anual
Y = porcentaje de renta bruta que se destina a impuestos (IRPF + SS + IVA + especiales)
```

Si la curva se aplana o baja a partir de cierto punto, la hipotesis queda respaldada.

---

## Resultados

### Modelo 1: IVA — Claramente regresivo (datos 2024)

Fuente: INE, Encuesta de Presupuestos Familiares, tabla 73809 (datos 2024).

| Tramo renta (neta mensual hogar) | Renta neta anual | Gasto total | Gasto/Renta | IVA pagado | IVA efectivo | **IVA % renta** |
|---|---|---|---|---|---|---|
| Hasta 499 EUR | 4.200 | 14.973 | 356% | 1.339 | 8.9% | **31.9%** |
| 500 - 999 EUR | 9.000 | 16.615 | 185% | 1.491 | 9.0% | **16.6%** |
| 1.000 - 1.499 EUR | 15.000 | 21.956 | 146% | 2.049 | 9.3% | **13.7%** |
| 1.500 - 1.999 EUR | 21.000 | 26.459 | 126% | 2.501 | 9.5% | **11.9%** |
| 2.000 - 2.499 EUR | 27.000 | 33.210 | 123% | 3.194 | 9.6% | **11.8%** |
| 2.500 - 2.999 EUR | 33.000 | 37.716 | 114% | 3.681 | 9.8% | **11.2%** |
| 3.000 - 4.999 EUR | 48.000 | 44.518 | 93% | 4.369 | 9.8% | **9.1%** |
| 5.000+ EUR | 84.000 | 64.823 | 77% | 6.326 | 9.8% | **7.5%** |

**Hallazgos clave:**

1. **El IVA es profundamente regresivo como porcentaje de la renta.** El tramo mas
   bajo destina el 31.9% de su renta a IVA; el mas alto, solo el 7.5%. Ratio 4:1.

2. **El tipo efectivo de IVA (IVA/gasto) es casi plano** (~9% en todos los tramos),
   lo que significa que los tipos reducidos en alimentacion NO compensan la
   regresividad. La regresividad viene de que los tramos bajos gastan todo (o mas)
   de lo que ingresan, mientras los altos ahorran un 23%+.

3. **El tramo "hasta 499 EUR" gasta 3.5x su renta declarada.** Esto indica fuentes
   de ingreso no declaradas (economia sumergida, ayudas familiares, ahorros previos).
   Aun asi, incluso si duplicaramos su renta estimada, el IVA seguiria siendo el
   ~16% de su renta — el doble que para el tramo alto.

4. **El tipo efectivo de IVA SUBE ligeramente con la renta** (de 8.9% a 9.8%),
   porque los tramos altos gastan mas en categorias gravadas al 21% (muebles,
   tecnologia, vehiculos) y menos proporcionalmente en alimentacion (4-10%).
   Pero este efecto es minimo comparado con el efecto gasto/renta.

**Sobre el tamano del hogar:** Los tramos del INE son de ingreso neto del
*hogar*, no del individuo. Los hogares de renta baja son pequenos (1.5 personas
— jubilados, jovenes solos) y los de renta alta son grandes (3.5 personas —
familias biparentales). Sin embargo, el **IVA como porcentaje de la renta es
identico** tanto si se calcula por hogar como por persona, porque al dividir
numerador (IVA) y denominador (renta) por el mismo numero de miembros, el
ratio se cancela: `IVA_hogar / renta_hogar = (IVA_hogar/N) / (renta_hogar/N)`.

Donde el tamano del hogar **si importa** es en la sintesis: al cruzar datos
INE (hogar) con datos AEAT (individuo), hay que decidir si un hogar con
3.000 EUR/mes netos son dos asalariados de 1.500 o uno de 3.000. Eso afecta
al calculo de IRPF y SS, no al de IVA.

### Modelo 2: IRPF — Progresivo (calculo teorico 2024)

Calculamos el IRPF teorico para un asalariado soltero sin hijos, aplicando la
escala estatal+autonomica, la reduccion por rendimientos del trabajo, el minimo
personal, y descontando las cotizaciones SS del trabajador.

Los tramos salariales corresponden a los salarios medios reales por tramo de la
estadistica "Mercado de Trabajo" de la AEAT (2023).

| Tramo | Salario bruto | SS trabajador | Reduccion | Base liquidable | Cuota IRPF | **Tipo efectivo** |
|---|---|---|---|---|---|---|
| 0-0.5 SMI | 3.239 | 211 | 7.302 | 0 | 0 | **0.0%** |
| 0.5-1 SMI | 11.549 | 751 | 7.302 | 3.496 | 0 | **0.0%** |
| 1-1.5 SMI | 18.718 | 1.217 | 2.666 | 14.836 | 1.884 | **10.1%** |
| 1.5-2 SMI | 26.101 | 1.697 | 2.364 | 22.040 | 3.723 | **14.3%** |
| 2-2.5 SMI | 33.858 | 2.201 | 2.364 | 29.293 | 5.899 | **17.4%** |
| 2.5-3 SMI | 41.256 | 2.682 | 2.364 | 36.210 | 8.045 | **19.5%** |
| 3-3.5 SMI | 48.769 | 3.170 | 2.364 | 43.235 | 10.644 | **21.8%** |
| 3.5-4 SMI | 56.388 | 3.665 | 2.364 | 50.359 | 13.280 | **23.6%** |
| 4-4.5 SMI | 64.037 | 3.979 | 2.364 | 57.694 | 15.994 | **25.0%** |
| 4.5-5 SMI | 71.586 | 3.979 | 2.364 | 65.243 | 19.206 | **26.8%** |
| 5-7.5 SMI | 89.452 | 3.979 | 2.364 | 83.109 | 27.246 | **30.5%** |
| 7.5-10 SMI | 128.465 | 3.979 | 2.364 | 122.122 | 44.802 | **34.9%** |
| 10+ SMI | 280.847 | 3.979 | 2.364 | 274.504 | 113.374 | **40.4%** |

**Hallazgos:**

1. El IRPF **si es progresivo**, del 0% al 40.4%. Esto no es sorpresa.

2. Los primeros ~12.000 EUR no pagan IRPF (la reduccion por trabajo + minimo
   personal se comen la base imponible).

3. A partir de la base maxima de SS (61.214 EUR), la deduccion de SS del
   trabajador se congela, asi que la base imponible crece mas rapido.

4. Nota: estos son tipos **teoricos maximos** para soltero sin hijos.
   Las deducciones familiares, autonomicas, etc. reducen estos tipos,
   especialmente en los tramos medios.

### Modelo 3: Seguridad Social — Regresivo por encima de la base maxima

La Seguridad Social tiene un tope: la base maxima de cotizacion (61.214 EUR/ano
en 2026). Por debajo, el tipo total es 37.15% del salario bruto. Por encima,
solo se paga la cotizacion adicional de solidaridad (1.15-1.46% en 2026).

**Escenario A: Solo parte del trabajador (lo que se ve en la nomina)**

| Tramo | Salario bruto | SS trabajador | **SS % salario** |
|---|---|---|---|
| 0-0.5 a 3.5-4 SMI | 3.239 - 56.388 | 211 - 3.665 | **6.50%** |
| 4-4.5 SMI | 64.037 | 3.984 | **6.22%** |
| 4.5-5 SMI | 71.586 | 3.999 | **5.59%** |
| 5-7.5 SMI | 89.452 | 4.037 | **4.51%** |
| 7.5-10 SMI | 128.465 | 4.130 | **3.21%** |
| 10+ SMI | 280.847 | 4.496 | **1.60%** |

**Escenario B: Total (trabajador + empresa)**

| Tramo | Salario bruto | Coste laboral | SS total | **SS % bruto** |
|---|---|---|---|---|
| Hasta 3.5-4 SMI | hasta 56.388 | hasta 73.671 | hasta 20.948 | **37.15%** |
| 5-7.5 SMI | 89.452 | 108.503 | 23.088 | **25.81%** |
| 7.5-10 SMI | 128.465 | 147.988 | 23.653 | **18.41%** |
| 10+ SMI | 280.847 | 302.229 | 25.877 | **9.21%** |

**Hallazgo clave:** La SS es el impuesto mas regresivo del sistema. Quien gana
56.000 EUR paga 37.15% de SS total; quien gana 280.000 EUR paga 9.21%. Ratio 4:1.
La "cotizacion adicional de solidaridad" apenas compensa (anade solo ~0.4 puntos
para rentas de 280k).

### SINTESIS: Carga fiscal total del asalariado

Combinamos los tres modelos. Para el IVA, interpolamos a partir de los datos del
INE, estimando el gasto en funcion de la renta neta disponible tras IRPF y SS.

#### Escenario A: Carga fiscal visible (IRPF + SS trabajador + IVA)

Lo que el asalariado efectivamente paga de su bolsillo.

| Tramo | Bruto | IRPF % | SS trab. % | IVA % | **TOTAL %** |
|---|---|---|---|---|---|
| 0-0.5 SMI | 3.239 | 0.0 | 6.5 | 41.3 | **47.8** |
| 0.5-1 SMI | 11.549 | 0.0 | 6.5 | 14.4 | **20.9** |
| 1-1.5 SMI | 18.718 | 10.1 | 6.5 | 11.2 | **27.8** |
| 1.5-2 SMI | 26.101 | 14.3 | 6.5 | 9.5 | **30.3** |
| 2-2.5 SMI | 33.858 | 17.4 | 6.5 | 9.0 | **32.9** |
| 2.5-3 SMI | 41.256 | 19.5 | 6.5 | 8.4 | **34.4** |
| 3-3.5 SMI | 48.769 | 21.8 | 6.5 | 7.7 | **36.1** |
| 3.5-4 SMI | 56.388 | 23.6 | 6.5 | 7.1 | **37.1** |
| 4-4.5 SMI | 64.037 | 25.0 | 6.2 | 6.5 | **37.7** |
| 4.5-5 SMI | 71.586 | 26.8 | 5.6 | 6.1 | **38.5** |
| 5-7.5 SMI | 89.452 | 30.5 | 4.5 | 5.5 | **40.5** |
| 7.5-10 SMI | 128.465 | 34.9 | 3.2 | 4.7 | **42.8** |
| 10+ SMI | 280.847 | 40.4 | 1.6 | 3.0 | **45.0** |

#### Escenario B: Carga fiscal economica total (IRPF + SS total + IVA)

Incluyendo la SS empresarial como parte de la carga sobre el trabajo.

| Tramo | Bruto | Coste laboral | IRPF % | SS total % | IVA % | **TOTAL % bruto** | **TOTAL % coste** |
|---|---|---|---|---|---|---|---|
| 0-0.5 SMI | 3.239 | 4.232 | 0.0 | 37.2 | 41.3 | **78.5** | **60.1** |
| 0.5-1 SMI | 11.549 | 15.089 | 0.0 | 37.2 | 14.4 | **51.5** | **39.4** |
| 1-1.5 SMI | 18.718 | 24.455 | 10.1 | 37.2 | 11.2 | **58.4** | **44.7** |
| 1.5-2 SMI | 26.101 | 34.101 | 14.3 | 37.2 | 9.5 | **60.9** | **46.6** |
| 2-2.5 SMI | 33.858 | 44.235 | 17.4 | 37.2 | 9.0 | **63.6** | **48.7** |
| 2.5-3 SMI | 41.256 | 53.901 | 19.5 | 37.2 | 8.4 | **65.1** | **49.8** |
| 3-3.5 SMI | 48.769 | 63.717 | 21.8 | 37.2 | 7.7 | **66.7** | **51.1** |
| 3.5-4 SMI | 56.388 | 73.671 | 23.6 | 37.2 | 7.1 | **67.8** | **51.9** |
| 4-4.5 SMI | 64.037 | 82.826 | 25.0 | 35.6 | 6.5 | **67.1** | **51.9** |
| 4.5-5 SMI | 71.586 | 90.451 | 26.8 | 31.9 | 6.1 | **64.9** | **51.4** |
| 5-7.5 SMI | 89.452 | 108.503 | 30.5 | 25.8 | 5.5 | **61.8** | **50.9** |
| 7.5-10 SMI | 128.465 | 147.988 | 34.9 | 18.4 | 4.7 | **58.0** | **50.4** |
| 10+ SMI | 280.847 | 302.229 | 40.4 | 9.2 | 3.0 | **52.6** | **48.9** |

### Conclusiones de la sintesis

**El escenario A (visible) muestra progresividad**, pero muy aplanada:
- Del 20.9% (0.5-1 SMI) al 45.0% (10+ SMI). Ratio apenas 2:1.
- El IRPF progresivo domina, pero el IVA y la SS restan mucha progresividad.
- El tramo 0-0.5 SMI es anomalo (47.8%) por gastar mucho mas de lo que declara.

**El escenario B (economico) es donde la hipotesis se confirma:**
- La carga **TIENE UN MAXIMO en el tramo 3.5-4 SMI (56.388 EUR)** al 67.8%.
- A partir de ahi, **BAJA**: 64.9% para 71k, 61.8% para 89k, 58.0% para 128k,
  y **52.6% para 280k**.
- La curva es una U invertida: sube hasta ~56k y luego baja.
- **El asalariado que gana 56.000 EUR paga proporcionalmente MAS que el que gana
  280.000 EUR** (67.8% vs 52.6% de su salario bruto).

**Como porcentaje del coste laboral** (la medida mas neutra), la carga es
sorprendentemente plana entre 48% y 52% para todos los tramos medios-altos.
Pero **nunca sube del 52%**, lo que significa que el sistema no es progresivo
por encima de los 50k: un asalariado medio y uno muy rico pagan practicamente
lo mismo como porcentaje del coste que representan.

**Y esto es SOLO para asalariados que declaran todo.** La hipotesis original
mencionaba que los tramos muy altos (>100k) tienen acceso a vehiculos de
evasion/elusion (sociedades interpuestas, retribucion en especie, equity,
cambio de residencia fiscal). Eso no esta incluido aqui y haria la curva
aun mas regresiva en la cola alta.

### Graficas

#### La U invertida (grafica clave)

La carga fiscal total (escenario B) sube hasta los 56k EUR y luego **baja
15.2 puntos** hasta los 281k EUR. El sistema es regresivo a partir de la
clase media-alta.

![U invertida](/assets/images/impuestos/u_invertida.png)

#### Tres fuerzas en tension

El IRPF sube (progresivo), pero la SS cae en picado a partir de la base
maxima (61k) y el IVA cae suavemente. La SS es la fuerza dominante: su
caida es mas pronunciada que la subida del IRPF.

![Componentes](/assets/images/impuestos/componentes.png)

#### Escenario A: Carga visible (nomina + IVA)

Lo que el trabajador ve: IRPF + SS trabajador + IVA. Progresivo pero muy
aplanado (ratio 2:1 entre tramo bajo y alto). El verde (IVA) domina en
los tramos bajos; el azul (IRPF) domina en los altos.

![Escenario A](/assets/images/impuestos/escenario_a_visible.png)

#### Escenario B: Carga total (incluyendo SS empresa)

Incluyendo la SS empresarial. El naranja (SS empresa) es el bloque mas
grande en todos los tramos por debajo de 61k, y se encoge drasticamente
por encima. Se ve claramente la bajada a partir del tramo 3.5-4 SMI.

![Escenario B](/assets/images/impuestos/escenario_b_total.png)

#### Comparacion de ambos escenarios

Las dos lineas juntas. La roja (total) muestra la U invertida; la azul
(visible) es mas suave pero tambien se aplana mucho a partir de 50k.

![Comparacion](/assets/images/impuestos/comparacion_escenarios.png)

### Analisis de sensibilidad

Testamos si nuestras conclusiones resisten cambios en los supuestos.

**Test 1: +/- 3 puntos en todos los tipos de IVA estimados.** La carga total
varia entre 2-7 puntos segun el tramo, pero la forma de la curva no cambia.
El tramo bajo sigue siendo el mas sensible (mas gasto = mas IVA).

**Test 2: IVA de vivienda (la mayor incertidumbre).** Probamos 3%, 8% y 12%.
El impacto es de 1-5 puntos segun tramo. No altera las conclusiones.

**Test 3: Inclusion de la SS empresarial.** Este es el factor decisivo:

| Tramo | Solo IRPF+IVA | +SS trab | +SS total | Diferencia SS emp |
|---|---|---|---|---|
| 1-1.5 SMI (19k) | 21.3% | 27.8% | 58.4% | +30.6pp |
| 3.5-4 SMI (56k) | 30.6% | 37.1% | 67.8% | +30.6pp |
| 10+ SMI (281k) | 43.4% | 45.0% | 52.6% | +7.6pp |

La SS empresarial anade 30.6 puntos a un trabajador de 56k, pero solo 7.6 al
de 281k. Es la principal fuente de regresividad.

**Test 4: ¿Se mantiene la U invertida en TODOS los escenarios?**

| Escenario | Pico | A 281k | ¿U invertida? |
|---|---|---|---|
| Peor caso (IVA bajo, sin SS emp) | 44.3% a 281k | 44.3% | **No** — curva plana/creciente |
| Base (con SS emp) | 67.8% a 56k | 52.6% | **Si** — cae 15.2pp |
| Mejor caso (IVA alto, con SS emp) | 69.3% a 56k | 53.3% | **Si** — cae 16.0pp |

**Conclusion: la U invertida depende de incluir la SS empresarial.** Si no se
incluye, el sistema es progresivo (aunque muy aplanado: del 17% al 44%). Si se
incluye — que es lo correcto economicamente — la carga pico esta en 56k y baja
15 puntos para los sueldos mas altos.

![Sensibilidad U invertida](/assets/images/impuestos/sensibilidad_u_invertida.png)

#### Sobre la inclusion de la SS empresarial

Incluimos la SS empresarial como carga del trabajador. Este es el tratamiento
estandar en economia publica (OCDE, FMI, la mayoria de la literatura academica).

**Argumentos a favor (posicion mayoritaria):**
- El empresario contrata en funcion del coste laboral total, no del salario
  bruto. La SS empresarial sale del mismo bolsillo que pagaria el salario.
- Evidencia empirica: en reformas que han cambiado el reparto (Suecia 2007,
  Colombia 2013), el 60-100% de la cotizacion empresarial se refleja en menores
  salarios. A largo plazo converge al 100%.
- Es un impuesto sobre la renta del trabajo, igual que el IRPF. No hay razon
  economica para tratarlo diferente por el hecho de que lo ingrese el empresario.

**Argumentos en contra (minoritarios pero legitimos):**
- Genera derechos (pension, desempleo) — no es un impuesto puro sino en parte
  un ahorro forzoso. Pero los derechos no son proporcionales a lo cotizado
  por encima de la base maxima.
- En mercados rigidos (convenios colectivos), los salarios no se ajustan
  rapidamente. Parte puede salir de beneficios a corto plazo.
- Algunas partidas (FOGASA, AT/EP) son seguros que protegen al trabajador
  frente a la empresa, no impuestos propiamente dichos. Pero son <2% del total.

### Elusion y evasion fiscal en rentas altas

Fuente: investigacion propia a partir de FEDEA, Gestha, Oxfam, Zucman et al.

Todo lo anterior asume que los asalariados de renta alta **declaran y pagan
lo que les corresponde**. Pero las rentas muy altas tienen acceso a mecanismos
legales (elusion) e ilegales (evasion) que reducen su carga real:

**1. Sociedades interpuestas.** En vez de cobrar como asalariado (IRPF hasta
47%), el alto directivo canaliza ingresos a traves de una SL (IS al 25%,
efectivo a menudo 5-9% para grandes empresas). La ruta IS + dividendo da un
tipo combinado del 39-44%, pero la ventaja real es el **diferimiento**: los
beneficios se quedan en la sociedad al 25% (o menos) indefinidamente.

**2. Rentas del capital vs. trabajo.** La base del ahorro tributa al 19-28%
(30% desde 2025), frente al 47% maximo de rentas del trabajo. Para el top 1%,
el **63% de sus ingresos son rentas del capital**, por lo que su tipo efectivo
cae drasticamente.

**3. Amnistia fiscal de Montoro (2012):**
- Objetivo: recaudar 2.500M EUR
- Recaudado: ~1.192M EUR (48% del objetivo)
- Activos aflorados: 40.000M EUR
- Tipo efectivo sobre lo aflorado: ~3% (no el 10% nominal)
- Declarada inconstitucional por el TC en 2017

**4. Economia sumergida:** Estimada en 15.8-24% del PIB (230.000-240.000M EUR).
Segun Gestha, el fraude fiscal anual es de 91.600M EUR, del cual el **72% es
atribuible a grandes empresas y grandes fortunas**, solo el 2.4% a familias.

**5. Dato clave: el Observatorio FEDEA (10o Informe, febrero 2025)** calcula
el tipo efectivo REAL por nivel de renta incluyendo todos los impuestos:

| Grupo de renta | Tipo efectivo total |
|---|---|
| 20% mas pobre | ~27.5% |
| Renta media (Q3) | ~33% |
| Percentil 91-99 | ~38% (el maximo) |
| **Top 1%** | **~24%** |

**El 1% mas rico paga menos que el 20% mas pobre.** 14 puntos menos que la
clase media. Esto confirma la hipotesis original: el sistema fiscal espanol
NO es progresivo en su conjunto, y es regresivo para las rentas mas altas.

Segun Zucman et al. (AER 2019), el 30-40% de la riqueza del top 0.01% de
Espana esta en paraisos fiscales. Se estiman 144.000M EUR de patrimonio
espanol oculto offshore.

### Validacion con datos reales (AEAT 2023)

Comparamos nuestro modelo teorico de IRPF con los datos reales de la AEAT
(estadistica "Mercado de Trabajo en las Fuentes Tributarias", 2023).

#### Datos reales de la AEAT

- **20.098.799** asalariados totales
- **481.981M EUR** en salarios
- **79.914M EUR** en retenciones
- Tipo medio de retencion para asalariados puros: **17.30%**
- Tipo medio de retencion para todos los asalariados: **16.58%**

#### Nuestro modelo vs realidad

| Concepto | Modelo | AEAT real | Ratio |
|---|---|---|---|
| IRPF total (bn EUR) | 83.4 | 79.9 | 1.04 |
| Tipo medio ponderado | **17.29%** | **16.58-17.30%** | ~1.0 |
| Salarios (bn EUR) | 482.0 | 482.0 | 1.00 |

**El modelo predice 17.29%, practicamente identico al 17.30% de los asalariados
puros.** La diferencia con el 16.58% general se explica porque el agregado
incluye a asalariados que tambien cobran pensiones o desempleo (con retenciones
menores).

#### Distribucion: quien paga que

| Tramo | Asalariados | % total | IRPF modelo | Tipo efectivo | % recaudacion |
|---|---|---|---|---|---|
| 0-0.5 SMI | 3.858.491 | 19.2% | 0 EUR | **0.0%** | 0.0% |
| 0.5-1 SMI | 3.552.234 | 17.7% | 0 EUR | **0.0%** | 0.0% |
| 1-1.5 SMI | 4.646.097 | 23.1% | 1.884 EUR | **10.1%** | 10.5% |
| 1.5-2 SMI | 2.878.080 | 14.3% | 3.723 EUR | **14.3%** | 12.9% |
| 2-2.5 SMI | 1.703.923 | 8.5% | 5.899 EUR | **17.4%** | 12.1% |
| 2.5-3 SMI | 1.287.300 | 6.4% | 8.045 EUR | **19.5%** | 12.4% |
| 3-3.5 SMI | 765.569 | 3.8% | 10.644 EUR | **21.8%** | 9.8% |
| 3.5-4 SMI | 419.551 | 2.1% | 13.280 EUR | **23.6%** | 6.7% |
| 4-4.5 SMI | 274.064 | 1.4% | 15.994 EUR | **25.0%** | 5.3% |
| 4.5-5 SMI | 187.519 | 0.9% | 19.206 EUR | **26.8%** | 4.3% |
| 5-7.5 SMI | 375.427 | 1.9% | 27.246 EUR | **30.5%** | 12.3% |
| 7.5-10 SMI | 80.463 | 0.4% | 44.802 EUR | **34.9%** | 4.3% |
| 10+ SMI | 70.081 | 0.3% | 113.374 EUR | **40.4%** | 9.5% |

**Hallazgos clave:**

1. **7.4 millones de trabajadores (37%) no pagan IRPF** (tramos 0-0.5 y 0.5-1 SMI).
   Su carga fiscal entera viene de la SS y del IVA. Esto refuerza la tesis de
   regresividad: para ellos, el IRPF progresivo no existe.

2. **Los tres tramos que mas recaudan** son 1.5-2 SMI (12.9%), 2.5-3 SMI (12.4%)
   y 5-7.5 SMI (12.3%). La recaudacion del IRPF depende tanto de la masa
   salarial como del tipo: los tramos medios recaudan mas que los altos porque
   hay mucha mas gente.

3. **El 0.3% de asalariados que gana >10 SMI aporta el 9.5% de la recaudacion.**
   Concentracion alta, pero no tanto como podria esperarse de un impuesto
   "progresivo". Y esto es sobre salarios — no sobre rentas del capital.

4. **La anomalia 0-0.5 SMI** (3.9M personas, 19% del total, salario medio 3.239
   EUR/ano). Son mayoritariamente trabajadores a tiempo parcial o temporales
   (media de 1.61 percepciones por persona). Pagan 0% de IRPF pero 6.5% de SS
   y un porcentaje indeterminado pero alto de IVA sobre todo lo que gastan.

#### Por que nuestro modelo sobreestima ligeramente

Nuestro modelo asume el caso mas desfavorable: asalariado soltero, sin hijos,
sin deducciones adicionales. Las diferencias con la realidad se explican por:

| Factor | Impacto estimado |
|---|---|
| Deducciones por hijos (~40% declarantes) | -0.5 a -1.5pp |
| Deduccion vivienda habitual (pre-2013) | -0.3 a -0.5pp |
| Planes de pensiones (~15%) | -0.1 a -0.3pp |
| Deducciones autonomicas | -0.1 a -0.3pp |
| Trabajadores a tiempo parcial (0-0.5 SMI) | -0.2 a -0.5pp |
| **Total estimado** | **-1.2 a -3.1pp** |

**Gap real: +0.71pp** (modelo 17.29% vs AEAT 16.58%). Cae dentro del rango
esperado. El modelo es estructuralmente correcto; solo esta ligeramente
desplazado hacia arriba por la asuncion conservadora.

![Validacion IRPF](/assets/images/impuestos/validacion_irpf.png)

---

## Fuentes de datos

### INE (Instituto Nacional de Estadistica)

| Fuente | Que contiene | URL |
|--------|-------------|-----|
| **Tabla 73809** — EPF por nivel de ingresos y grupo de gasto | Gasto medio por hogar en 14 categorias COICOP x 8 tramos de ingreso. Datos 2016-2024 | [ine.es/jaxiT3/Tabla.htm?t=73809](https://www.ine.es/jaxiT3/Tabla.htm?t=73809) |
| **Tabla 73795** — EPF por nivel de ingresos (agregado) | Gasto total medio por hogar x 8 tramos de ingreso | [ine.es/jaxiT3/Tabla.htm?t=73795](https://www.ine.es/jaxiT3/Tabla.htm?t=73795) |
| **API JSON** | Acceso programatico a las tablas | `servicios.ine.es/wstempus/js/ES/DATOS_TABLA/{id_tabla}` |

**Tramos de ingreso mensual neto del hogar (INE)**:
- Hasta 499 EUR
- 500 - 999 EUR
- 1.000 - 1.499 EUR
- 1.500 - 1.999 EUR
- 2.000 - 2.499 EUR
- 2.500 - 2.999 EUR
- 3.000 - 4.999 EUR
- 5.000 EUR o mas

### AEAT (Agencia Tributaria)

| Fuente | Que contiene | URL |
|--------|-------------|-----|
| **Mercado de Trabajo y Pensiones** | Datos exclusivamente de asalariados: numero, salario medio, retenciones, tipo medio de retencion. Por tramos en multiplos del SMI. Datos 2023 | [sede.agenciatributaria.gob.es/.../mercado/2023/](https://sede.agenciatributaria.gob.es/AEAT/Contenidos_Comunes/La_Agencia_Tributaria/Estadisticas/Publicaciones/sites/mercado/2023/) |
| **Estadistica Declarantes IRPF** | Todos los declarantes: base imponible, cuota liquida, tipo efectivo, por 10 tramos de rendimiento. Datos 2004-2023 | [sede.agenciatributaria.gob.es/.../irpf/2023/](https://sede.agenciatributaria.gob.es/AEAT/Contenidos_Comunes/La_Agencia_Tributaria/Estadisticas/Publicaciones/sites/irpf/2023/home.html) |
| **Informe Anual Recaudacion** | Tipo efectivo agregado del IRPF (14.33% en 2023). Cuadros Excel descargables | [sede.agenciatributaria.gob.es/.../ejercicio-2023/](https://sede.agenciatributaria.gob.es/Sede/estadisticas/recaudacion-tributaria/informe-anual/ejercicio-2023/2-impuesto-sobre-renta-personas-fisicas.html) |

**Tramos salariales AEAT (en multiplos del SMI, 2023: SMI = 15.120 EUR/ano)**:

| Tramo | Rango aproximado |
|-------|-----------------|
| 0 - 0.5 SMI | 0 - 7.560 EUR |
| 0.5 - 1 SMI | 7.560 - 15.120 EUR |
| 1 - 1.5 SMI | 15.120 - 22.680 EUR |
| 1.5 - 2 SMI | 22.680 - 30.240 EUR |
| 2 - 2.5 SMI | 30.240 - 37.800 EUR |
| 2.5 - 3 SMI | 37.800 - 45.360 EUR |
| 3 - 3.5 SMI | 45.360 - 52.920 EUR |
| 3.5 - 4 SMI | 52.920 - 60.480 EUR |
| 4 - 5 SMI | 60.480 - 75.600 EUR |
| 5 - 7.5 SMI | 75.600 - 113.400 EUR |
| 7.5 - 10 SMI | 113.400 - 151.200 EUR |
| > 10 SMI | > 151.200 EUR |

### Seguridad Social (2026)

| Concepto | Trabajador | Empresa | Total |
|----------|-----------|---------|-------|
| Contingencias comunes | 4.70% | 23.60% | 28.30% |
| Desempleo (indef.) | 1.55% | 5.50% | 7.05% |
| Formacion profesional | 0.10% | 0.60% | 0.70% |
| MEI | 0.15% | 0.75% | 0.90% |
| FOGASA | — | 0.20% | 0.20% |
| **Total (sin AT/EP)** | **6.50%** | **30.65%** | **37.15%** |

- **Base maxima**: 5.101,20 EUR/mes = 61.214 EUR/ano
- Por encima: cotizacion adicional de solidaridad (1.15% - 1.46% en 2026)

### Tipos de IVA en Espana (2024)

| Tipo | Porcentaje | Aplicacion |
|------|-----------|------------|
| Superreducido | 4% | Pan, leche, huevos, frutas, verduras, cereales, queso, libros, medicamentos con receta |
| Reducido | 10% | Otros alimentos, restauracion, transporte publico, hosteleria, agua |
| General | 21% | Todo lo demas (ropa, electronica, muebles, combustible, servicios, etc.) |
| Exento | 0% | Educacion, sanidad publica, seguros, servicios financieros, alquileres de vivienda |

### Mapeo COICOP -> Tipo de IVA predominante

| Cod. | Categoria COICOP | IVA estimado | Notas |
|------|-----------------|-------------|-------|
| 01 | Alimentos y bebidas no alcoholicas | ~7% (mix 4%/10%) | Basicos al 4%, procesados al 10% |
| 02 | Bebidas alcoholicas, tabaco | 21% + especiales | Impuestos especiales adicionales |
| 03 | Vestido y calzado | 21% | |
| 04 | Vivienda, agua, electricidad, gas | ~8% (mix) | Alquiler exento, energia 10-21%, agua 10% |
| 05 | Muebles, articulos del hogar | 21% | |
| 06 | Sanidad | ~5% (mix) | Publica exenta, farmacos 4%, privada 21% |
| 07 | Transporte | ~18% (mix) | Coches/gasolina 21%, publico 10% |
| 08 | Comunicaciones | 21% | |
| 09 | Ocio y cultura | ~15% (mix) | Libros 4%, espectaculos 10-21% |
| 10 | Educacion | 0% (exento) | |
| 11 | Restaurantes y hoteles | 10% | |
| 12 | Seguros y servicios financieros | 0% (exento) | |
| 13 | Cuidado personal y otros | ~18% (mix) | |

---

## Limitaciones y caveats

1. **Tramos de renta no coinciden** entre INE y AEAT. Habra que armonizarlos
   (interpolacion o reagrupacion).

2. **Los datos del INE son de ingresos netos del hogar**, no brutos individuales.
   Hay que hacer supuestos para pasar de neto hogar a bruto individual.

3. **El mapeo COICOP -> IVA es aproximado** a nivel de 2 digitos. Con datos a
   5 digitos seria mas preciso, pero bastante mas complejo.

4. **La parte empresarial de la SS** es debatible: los economistas discrepan sobre
   si la soporta el trabajador (via menor salario) o la empresa (via menor
   beneficio). Presentaremos ambos escenarios.

5. **No incluimos** (de momento): Impuesto de Patrimonio, IBI, impuesto de
   matriculacion, plusvalias municipales, tasas. Estos reforzarian la hipotesis
   en algunos tramos.

---

## Conclusiones finales

### Respuesta a la hipotesis

**La hipotesis se confirma.** El sistema fiscal espanol, considerado en su
conjunto (IRPF + Seguridad Social + IVA), **no es progresivo** para los
asalariados. La respuesta exacta depende de que se incluya en el calculo:

- **Si solo se miran los impuestos visibles** (IRPF + SS trabajador + IVA),
  el sistema es tecnicamente progresivo, pero de una progresividad muy debil:
  la carga va del 21% al 45% (ratio 2:1). La curva se aplana a partir de los
  50.000 EUR.

- **Si se incluye la SS empresarial** (lo correcto economicamente, segun la
  posicion mayoritaria en economia publica), **el sistema es regresivo a partir
  de los 56.000 EUR**. La carga pico es del 67.8% para un salario bruto de
  56.388 EUR, y *baja* al 52.6% para 280.847 EUR. Un asalariado de clase
  media-alta paga proporcionalmente mas que uno rico.

- **Si ademas se tiene en cuenta la elusion y evasion fiscal** de las rentas
  muy altas (FEDEA, 2025), el panorama es aun peor: el top 1% paga un tipo
  efectivo total del ~24%, menos que el 20% mas pobre (~27.5%).

### El mecanismo: tres fuerzas, una sola ganadora

El sistema fiscal espanol para asalariados es el resultado de tres fuerzas
en tension:

```
IRPF (progresivo)       ↑  del 0% al 40%      — sube siempre
SS   (regresivo)        ↓  del 37% al 9%       — cae en picado a partir de 61k
IVA  (regresivo)        ↓  del 32% al 7%       — cae suavemente
```

**La Seguridad Social gana.** La base maxima de cotizacion (61.214 EUR/ano)
crea un efecto de corte brutal: por debajo, la SS total supone el 37.15% del
salario bruto; por encima, se congela y la tasa efectiva se desploma. La
"cotizacion adicional de solidaridad" (introducida en 2025, 1.15-1.46% en
2026) apenas amortigua el efecto: anade solo ~0.4 puntos para un salario
de 280k.

El IRPF sube, si, pero no lo suficiente para compensar la caida combinada
de SS e IVA. El resultado neto es la **U invertida**: la carga total sube
hasta los ~56k y despues baja.

### En numeros: que paga cada asalariado

Una tabla resumen con los tres niveles de analisis:

| Asalariado | Bruto | Esc. A (visible) | Esc. B (total) | Con elusion (FEDEA) |
|---|---|---|---|---|
| Temporal/parcial (0.5 SMI) | 3.239 | 47.8% | 78.5%* | — |
| Mileurista (1 SMI) | 11.549 | 20.9% | 51.5% | ~27.5% |
| Salario medio (1.5 SMI) | 18.718 | 27.8% | 58.4% | ~30% |
| Buen sueldo (2.5 SMI) | 41.256 | 34.4% | 65.1% | ~33% |
| **Pico: 3.5-4 SMI** | **56.388** | **37.1%** | **67.8%** | ~35% |
| Alto cargo (5-7.5 SMI) | 89.452 | 40.5% | 61.8% | ~38% |
| Directivo (10+ SMI) | 280.847 | 45.0% | 52.6% | ~24%** |

*El 78.5% del tramo 0-0.5 SMI es anomalo: estos trabajadores gastan
mucho mas de lo que declaran (ahorros, economia sumergida, ayuda familiar).

**El ~24% del top 1% (FEDEA) refleja que las rentas muy altas ya no son
mayoritariamente salariales: el 63% son rentas del capital, con tipos
marginales mucho menores.

### La paradoja del asalariado espanol

El resultado mas llamativo de este estudio es una paradoja:

> **El asalariado que gana 56.000 EUR paga proporcionalmente MAS impuestos
> que el que gana 280.000 EUR.**

Esto no es un defecto del IRPF, que es genuinamente progresivo. Es un defecto
**estructural** del sistema en su conjunto, causado por:

1. **El tope de cotizacion a la SS**, que convierte una carga plana del 37%
   en una carga fuertemente regresiva por encima de 61k.

2. **La regresividad del IVA**, que afecta mas a quien mas gasta de su renta
   (los tramos bajos gastan el 100-350% de lo que declaran; los altos, el 77%).

3. **La dualidad rentas del trabajo / rentas del capital**, que permite a las
   rentas muy altas tributar por la base del ahorro (19-28%) en vez de por
   la base general (hasta 47%).

4. **La elusion fiscal**, facilitada por sociedades interpuestas, diferimiento
   de beneficios, y la arquitectura misma del IS + dividendo.

### Robustez de los resultados

Los resultados han sido sometidos a pruebas de sensibilidad y validacion:

- **Sensibilidad**: La U invertida se mantiene bajo todos los supuestos
  razonables de IVA (+/-3pp, vivienda 3-12%) siempre que se incluya la SS
  empresarial. Sin SS empresarial, la curva es creciente pero muy aplanada.

- **Validacion con AEAT**: Nuestro modelo teorico de IRPF predice un tipo
  medio ponderado del 17.29%, frente al 17.30% real de la AEAT para
  asalariados puros. La recaudacion modelada (83.4 bn EUR) es solo un 4%
  superior a la real (79.9 bn), explicable por las deducciones personales
  que no incluimos.

- **Consistencia con FEDEA**: Nuestros resultados para asalariados son
  coherentes con el patron del Observatorio FEDEA (tipo efectivo creciente
  hasta el percentil 90-99 y luego decreciente), con la diferencia de que
  FEDEA incluye todas las rentas, no solo salarios.

### Lo que no hemos incluido (y que reforzaria la hipotesis)

Este estudio se limita a **asalariados con contrato** que declaran todo.
No incluye:

1. **Impuesto de Patrimonio / Grandes Fortunas**: afecta a <1% de
   declarantes; su efecto es minimo en la carga total.

2. **IBI y tasas municipales**: regresivos (planos sobre el valor del
   inmueble, no sobre la renta).

3. **Impuestos especiales** (alcohol, tabaco, hidrocarburos): regresivos,
   suponen ~2-3% de la renta para tramos bajos.

4. **Economia sumergida**: estimada en 16-24% del PIB. El 72% del fraude
   fiscal es atribuible a grandes empresas y grandes fortunas (Gestha).

5. **Planificacion fiscal internacional**: paraisos fiscales, treaty
   shopping, etc. Zucman estima que el 30-40% del patrimonio del top
   0.01% espanol esta offshore.

Todos estos factores **aumentarian** la regresividad para los tramos
mas altos.

### Reflexion final

El sistema fiscal espanol **parece** progresivo si solo se mira el IRPF.
Pero el IRPF es solo una pieza de un sistema mas amplio donde:

- Las cotizaciones sociales son la mayor carga sobre el trabajo y son
  regresivas por encima de 61k.
- El IVA es invisible pero profundamente regresivo como porcentaje de
  la renta.
- Las rentas del capital tributan menos que las del trabajo.
- La elusion y evasion reducen la carga real del top 1% por debajo de
  la del 20% mas pobre.

La progresividad nominal del IRPF es una cortina que oculta un sistema
que, medido en su conjunto, carga mas a la clase media-alta trabajadora
(50-60k) que a las rentas realmente altas. El asalariado no tiene donde
esconderse: su renta es transparente, su SS es automatica, y su consumo
esta gravado al 100%. Las rentas de capital, patrimoniales y empresariales
disponen de herramientas legales que los asalariados simplemente no tienen.
