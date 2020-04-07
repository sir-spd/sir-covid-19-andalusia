# COVID-19 SIR mathematical model for Andalusia

SIR mathematical model for infectious diseases optimized for COVID-19 using Spanish Ministry of Health public available data for Andalusia.

-----

![sir-cases](https://github.com/agastalver/sir-covid-19-andalusia/raw/master/images/generated-sir-cases.png "SIR Model Cases")

![sir](https://github.com/agastalver/sir-covid-19-andalusia/raw/master/images/generated-sir.png "SIR Model")

**Note**: 

* `susceptible`, `infected`, and `recovered`, stand for the observable population; thus, the ones that can be detected. The actual values could be higher.
* `susceptible` is an estimated value calculated from `N` with respect to the `infected` and `recovered`, the actual value is not provided by the government.
* `recovered` stands for people who has recovered from the virus or has died; as considered in the SIR model.

-----

## Last optimization

### Case forecasting table

| Date           | Infected | Cases    |
|:--------------:|:--------:|:--------:|
| 2020-04-07     | 7540     | 8802     |
| 2020-04-08     | 7642     | 9011     |
| 2020-04-09     | 7711     | 9189     |
| 2020-04-10     | 7752     | 9340     |
| **2020-04-11** | **7769** | **9466** |
| 2020-04-12     | 7765     | 9572     |
| 2020-04-13     | 7744     | 9661     |
| 2020-04-14     | 7709     | 9735     |
| 2020-04-15     | 7662     | 9797     |
| 2020-04-16     | 7606     | 9849     |
| 2020-04-17     | 7542     | 9892     |
| 2020-04-18     | 7472     | 9928     |
| 2020-04-19     | 7397     | 9958     |
| 2020-04-20     | 7318     | 9984     |

### Optimized SIR parameters

```
N = 10122.328593664532
beta = 0.2718764487497858
gamma = 0.014003401700079816
delta = 0.8380326716279755
delay = 0
```

* `delta` stands for a factor of reduction of `beta` during the lockdown.
* All results are available in the folders `images` and `data`.

-----

## Last data information

### Andalusia total cases

![total](https://github.com/agastalver/sir-covid-19-andalusia/raw/master/images/generated-total.png "Total cases")

-----

## Methodology

### Data sources

Main data source:

* Spanish government: https://www.mscbs.gob.es/profesionales/saludPublica/ccayes/alertasActual/nCov-China/situacionActual.htm
  * https://covid19.isciii.es/
  * https://covid19.isciii.es/resources/serie_historica_acumulados.csv

* Github: https://github.com/datadista/datasets
  * https://raw.githubusercontent.com/datadista/datasets/master/COVID%2019/ccaa_covid19_casos_long.csv
  * https://raw.githubusercontent.com/datadista/datasets/master/COVID%2019/ccaa_covid19_altas_long.csv
  * https://raw.githubusercontent.com/datadista/datasets/master/COVID%2019/ccaa_covid19_fallecidos_long.csv

### Epidemiology model

This is based on the SIR epidemiology model proposed by W. O. Kermack and A. G. McKendrick in:

```
Kermack, W. O.; McKendrick, A. G. (1927). "A Contribution to the Mathematical Theory of Epidemics". Proceedings of the Royal Society A: Mathematical, Physical and Engineering Sciences. 115 (772): 700. Bibcode:1927RSPSA.115..700K. doi:10.1098/rspa.1927.0118. JSTOR 94815.
```

You can find the description on wikipedia: https://en.wikipedia.org/wiki/Mathematical_modelling_of_infectious_disease#The_SIR_model

### Optimization

The parameters `N`, `beta`, and `gamma`, are unknown. Additionally, a `delay` parameter is considered; defined as a time synchronization parameter in case the available data is not adjusted to day 0.

The optimization method is Nendel-Mead, adjusting mean squares on `I(t)` and `R(t)` to the available data. `S(t)` and `N` are calculated backwards.

```
Nelder, John A.; R. Mead (1965). "A simplex method for function minimization". Computer Journal. 7 (4): 308–313. doi:10.1093/comjnl/7.4.308.
```

## Usage

Execute:

```
$ python main.py
```

## Important note

The mathematical model could not adjust to the real behaviour of the virus. Furthermore, the data can have errors, delays, or be incomplete, so the adjustment can vary in the future.
