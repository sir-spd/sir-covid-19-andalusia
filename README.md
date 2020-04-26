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
| 2020-04-26     | 6809     | 12000    |
| 2020-04-27     | 6667     | 12012    |
| 2020-04-28     | 6525     | 12020    |
| 2020-04-29     | 6384     | 12026    |
| 2020-04-30     | 6245     | 12031    |
| 2020-05-01     | 6108     | 12034    |
| 2020-05-02     | 5973     | 12037    |
| 2020-05-03     | 5840     | 12038    |
| 2020-05-04     | 5710     | 12040    |
| 2020-05-05     | 5582     | 12041    |
| 2020-05-06     | 5458     | 12042    |
| 2020-05-07     | 5335     | 12042    |

### Optimized SIR parameters

```
N = 12045.243408585367
beta = 0.3006577419912406
gamma = 0.022575015548053523
delta = 0.6529688310812012
epsilon = 1.757291691903319
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
