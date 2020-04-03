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

| Date           | Infected  | Cases      |
|:--------------:|:---------:|:----------:|
| 2020-04-03     | 6844      | 7511       |
| 2020-04-04     | 7186      | 7931       |
| 2020-04-05     | 7485      | 8313       |
| 2020-04-06     | 7742      | 8654       |
| 2020-04-07     | 7957      | 8956       |
| 2020-04-08     | 8133      | 9221       |
| 2020-04-09     | 8272      | 9452       |
| 2020-04-10     | 8378      | 9650       |
| 2020-04-11     | 8454      | 9820       |
| 2020-04-12     | 8505      | 9965       |
| 2020-04-13     | 8567      | 10122      |
| 2020-04-14     | 8599      | 10249      |
| **2020-04-15** | **8605**  | **10351**  |
| 2020-04-16     | 8591      | 10432      |
| 2020-04-17     | 8561      | 10497      |
| 2020-04-18     | 8518      | 10550      |
| 2020-04-19     | 8466      | 10591      |
| 2020-04-20     | 8405      | 10625      |
| 2020-04-21     | 8339      | 10651      |
| 2020-04-22     | 8268      | 10673      |
| 2020-04-23     | 8194      | 10690      |

### Optimized SIR parameters

```
N = 10763.321593463046
beta = 0.2731686648181352
gamma = 0.010991386645253707
delta = 0.7683295256154763
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
