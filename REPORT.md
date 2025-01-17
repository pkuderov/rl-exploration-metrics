
# №43: Exploration Metrics for RL agents.

Авторы: ***Нестерова Мария** (ФИЦ ИУ РАН, аспирант МФТИ), **Загайнов Никита** (Innopolis University), **Манжос Геннадий** (Приволжский исследовательский медицинский университет, аспирант университета ИТМО)*

##



## Методы
Было выдвинуто предположение, что существующие методы исследования, такие как **RND, Model Disagreement as intrinsic reward, Entropy**, плохо работают при масштабировании среды агента или полной её замены. Для проведения экспериментов, мы использовали метрики:

**State Counting** - это когда мы считаем общее кол-во посещенных агентом клеток в заданной среде и строим частоту посещений определенных клеток в виде тепловой карты.
![state-counting](public/state-counting.png)
 https://www.sciencedirect.com/science/article/pii/S1566253522000288?via%3Dihub#b14

**RND** - это когда агент получает внутреннюю мотивацию **(intrinsic reward)** за ход, приближающий его ближе к вознаграждению 
![rnd](public/rnd.png)
 [https://arxiv.org/pdf/1810.12894](https://arxiv.org/pdf/1810.12894)

**Model Disagreement** - это когда агент получает внутреннюю мотивацию **(intrinsic reward)** за ход, приближающий его ближе к вознаграждению 
![model-disagreement](public/model-disagreement.png)
[https://pathak22.github.io/exploration-by-disagreement/resources/icml19.pdf](https://pathak22.github.io/exploration-by-disagreement/resources/icml19.pdf)

**Offline Measures for Exploration** - это офлайн-оценка того, насколько близко распределение собранных состояний к равномерному распределению.
![dist-metric](public/dist-metric.png)
[https://arxiv.org/pdf/2010.15533](https://arxiv.org/pdf/2010.15533)

## Разработка

Для обучения агента был использован метод **PPO**. Мы использовали фреймворк **cleanRL** (https://docs.cleanrl.dev/) для создания основного пайплайна быстрой воспроизводимости результатов эксперимента, **tensorboard** (https://www.tensorflow.org/tensorboard) и **wandb** (https://wandb.ai/site) для трекинга графиков экспериментов. 

### Среды
В данной работе мы исследовали существующие метрики для различных популярных сред в обучении с подкреплением, используя фреймворк gymnasium для выбора сред, таких как **PointMaze, AntMaze, MontezumaRevenge** (https://robotics.farama.org/envs/maze/, https://gymnasium.farama.org/environments/atari/montezuma_revenge/). 

Для создания пайплайна всех экспериментов, мы использовали код алгоритма **PPO**, дополнив в нём соответствующие параметры запуска сред с нужными нам флагами: выбор нужной среды (pointmaze, antmaze, montezuma revenge), выбор размера карт с параметрами small (7x10) | medium (15x15) | large (25x25). 

Таким образом, были созданы кастомные карты сред-лабиринтов в виде матриц, с явно заданными целями **"g" (goal)** и **"r" (agent)**. 

#### PointMaze
![point-maze-gif](public/point-maze.gif)

#### AntMaze
![ant-maze-gif](public/ant-maze.gif)

#### MontezumaRevenge
![montezume-revenge-gif](public/montezuma-revenge.gif)

## Эксперименты

Сперва мы запустили пайплайн со средой **PointMaze**, получив следующие результаты:

![point-maze](public/point-maze.png)

Затем, мы запустили тот же пайплайн со средой **AntMaze**, получив следующие результаты:

![ant-maze](public/ant-maze.png)

В конце, мы запустили тот же пайплайн со средой **MontezumaRevenge**, получив следующие результаты:

![montezuma-revenge](public/montezuma-revenge.png)

В последние минуты мы запустили оффлайн-тестирование метрики на основе распределений на **PointMaze**. Результаты:

![dist-point-maze](public/dist-point-maze.png)

## Результаты

По итогам проведенной работы, можно сказать о том, что описанные здесь подходы при выборе разных сред показывают что подходы, основанные на оценке новизны, иногда обеспечивают достойную оценку исследования агента RL, но они недостаточно подтверждены, чтобы обобщить этот ответ на все среды и алгоритмы.









