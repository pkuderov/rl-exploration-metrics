# Запуск минимально-рабочего сэтапа

```shell
cd ~/nikita
conda activate ./.conda
cd project
python ppo_experiments.py
```

```shell
python ppo_experiments.py --use_rnd_metric --use_state_counting_metric --track
```

Мониторить нагрузку
CPU: `htop`
GPU: `watch -n 1 nvidia-smi `

Аргументы для выбора кастомных карт (из maze_maps.py): `--env_map=small|medium|large`

```python ppo_experiments.py --use_state_counting_metric --save_history_of_obs --wandb_project_name="cleanRL-distr-metric" --track```