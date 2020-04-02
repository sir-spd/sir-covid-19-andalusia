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
| 2020-04-02     | 6452      | 7048       |
| 2020-04-03     | 6836      | 7505       |
| 2020-04-04     | 7180      | 7928       |
| 2020-04-05     | 7481      | 8311       |
| 2020-04-06     | 7740      | 8655       |
| 2020-04-07     | 7957      | 8960       |
| 2020-04-08     | 8134      | 9227       |
| 2020-04-09     | 8275      | 9459       |
| 2020-04-10     | 8382      | 9659       |
| 2020-04-11     | 8460      | 9831       |
| 2020-04-12     | 8512      | 9978       |
| 2020-04-13     | 8575      | 10137      |
| 2020-04-14     | 8607      | 10265      |
| **2020-04-15** | **8614**  | **10368**  |
| 2020-04-16     | 8601      | 10451      |
| 2020-04-17     | 8571      | 10517      |
| 2020-04-18     | 8529      | 10570      |
| 2020-04-19     | 8476      | 10612      |
| 2020-04-20     | 8416      | 10646      |
| 2020-04-21     | 8349      | 10673      |
| 2020-04-22     | 8278      | 10695      |
| 2020-04-23     | 8203      | 10712      |

### Optimized SIR parameters

```
N = 10787.061909393004
beta = 0.2730366919758111
gamma = 0.011050376961748555
delta = 0.7678320163629395
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
