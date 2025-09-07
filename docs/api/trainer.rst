Trainer Interface
================================

Last updated: 06/08/2025 (API docstrings are auto-generated).

Trainers drive the training loop. Introducing new trainer classes in case of new training paradiam is encouraged.

.. autosummary::
   :nosignatures:

   verl.trainer.ppo.ray_trainer.RayPPOTrainer


Core APIs
~~~~~~~~~~~~~~~~~

.. autoclass:: verl.trainer.ppo.ray_trainer.RayPPOTrainer
   :members: __init__, init_workers, fit

.. automodule:: verl.utils.tokenizer
   :members: hf_tokenizer

.. automodule:: verl.trainer.ppo.core_algos
   :members: agg_loss, kl_penalty, compute_policy_loss, kl_penalty

.. automodule:: verl.trainer.ppo.reward
   :members: load_reward_manager, compute_reward, compute_reward_async

.. autoclass:: verl.workers.reward_manager.NaiveRewardManager

.. autoclass:: verl.workers.reward_manager.DAPORewardManager
Examples
-----------------

- Minimal end-to-end PPO training driver snippet (single node Ray):

.. code-block:: python

   from omegaconf import OmegaConf
   from verl.trainer.ppo.ray_trainer import RayPPOTrainer, ResourcePoolManager
   from verl.trainer.ppo.utils import Role, WorkerType
   from verl.workers.fsdp_workers import ActorRolloutRefWorker, CriticWorker

   cfg = OmegaConf.load("examples/ppo_trainer/config.yaml")
   rpm = ResourcePoolManager(
       resource_pool_spec={"default": [4]},
       mapping={Role.ActorRollout: "default", Role.Critic: "default"},
   )
   role_map = {Role.ActorRollout: WorkerType.FSDP, Role.Critic: WorkerType.FSDP}
   trainer = RayPPOTrainer(cfg, tokenizer=None, role_worker_mapping=role_map, resource_pool_manager=rpm)
   trainer.init_workers()
   trainer.fit()
