# Nanodegree Machine Learning Engineer 

## Final project proposal 
Leticia Portella
July 21st, 2018

## Proposal

### Subject History and problem description

The brazilian roads are very dangerous being responsible for several deaths 
through the years. The responsabilities of the roads are splited in local, regional and 
national polices. The National Road Police has open data of all accidents that 
happened on federal roads and their main characteristics.   

These are some news about road accidents in Brazil: 

* [Brasil é o quinto país do mundo em mortes no trânsito, segundo OMS](https://www.metrojornal.com.br/foco/2017/05/01/brasil-e-o-quinto-pais-mundo-em-mortes-no-transito-segundo-oms.html)
* [Trânsito no Brasil mata 47 mil por ano e deixa 400 mil com alguma sequela](https://www1.folha.uol.com.br/seminariosfolha/2017/05/1888812-transito-no-brasil-mata-47-mil-por-ano-e-deixa-400-mil-com-alguma-sequela.shtml)
* [Acidentes de trânsito custam R$ 19 bi por ano, e Brasil fica longe de meta](https://www1.folha.uol.com.br/cotidiano/2017/11/1932336-acidentes-de-transito-custam-r-19-bi-por-ano-e-brasil-fica-longe-de-meta.shtml)

The main idea of the project is try to estimate what kind of victims an accident can 
cause based on road characteristics and climate conditions in the time of the accident.
If the type of victims can be predicted, it means we can analyze the most dangerous 
roads and climate characteristics. 

Similar analysis can be checked [here](http://ajith.softcomputing.net/isda-mam.pdf).


### Dataset 

The dataset was collected on the 
[site of the National Road Police](https://www.prf.gov.br/portal/dados-abertos).
I will the datasets from 2017 and 2016 with the current variables available:

* id - accident identification
* data_inversa - accident date
* dia_semana - weekday of the accident
* horario - time of the accident
* uf - state of the road
* br - federal road number
* km - kilometer of the road where the accident took place
* municipio - county where the accident took place
* causa_acidente - accident cause
* tipo_acidente - kind of accident
* classificacao_acidente - if the accident had victims (with injured victims, with deaths, without victims)
* fase_dia - time of day the accident happened (day, night, dawn, dusk)
* sentido_via - road direction on the point where the accident happened (ascending, descending, not specified)
* condicao_metereologica - meteorological condition
* tipo_pista - kind of road (single, double, multiple)
* tracado_via - road layout (tunnel, curve, straight, etc...)
* uso_solo - if the soil is being used (yes/no)
* pessoas - number of people involved
* mortos - number of dead people
* feridos_leves - number of people with small injuries
* feridos_graves - number of people with severe injuries
* ilesos - number of unharmed people
* ignorados - number of people involved but with no information of injuries
* feridos - number of all injuried people
* veiculos - number of veicules
* latitude
* longitude


### Solution description 

The target variable (`classificacao_acidente`) is a categorical variable. Thus, 
it will be converted to the following numbers:

* Class 0 - Car accidents with no victims
* Class 1 - Car accidents with injured victims
* Class 2 - Car accidents with death victims

This way, the model must be a supervised machine learning algorithm that will 
try to define which class the accident will likely fall given the roads and climate 
conditions.


### Benchmark

[Chong, Abraham & Paprzycki, 2005](http://ajith.softcomputing.net/isda-mam.pdf) 
did a simillar study, where they used neural network for trying to classify 
victims degree of injuries on traffic accidents. On this study, they had 5 classes 
of injures, including `no injury`, `possible injury`, `non-incapacitating injury`, 
`incapacitating injury`, and `fatal injury`. 
The features where based both on road and driver's characteristics. The road 
characteristics were similiar to what we found in the datasets of National Road Police.
The authors found a ~60% accuracy on predicting 

### Evaluation metrics 

I intend to use confunsion matrix, as explained 
[on this post](http://scikit-learn.org/stable/auto_examples/model_selection/plot_confusion_matrix.html),
 as well as f1_scores, recall and precision. In this case, I would prioritize 
the recall values, since a `false negative` is worse than a `false positive`. This 
is because if an accident predicted `injuries` instead of `no injuries`, it would 
mean that the road should be considered dangerous (which is not a bad final result). 
However, when a result has a `false negative`, it indicated that a potentially 
dangerous road was not classified as a dangerous one.

### Project design 

The project will be devided as described, based on 
[cookiecutter-data-science](https://drivendata.github.io/cookiecutter-data-science/):

* A `data` folder containing the csvs files
* A `notebooks` folder containing the notebooks on insights and model training
* A `model` folder containing the final version of the model
* A `requirements.txt` with software requirements for this project

By the end of the project, I will like to have a model that has a good accuracy 
on predicting the type of victims, indicating the most dangerous roads and conditions.
