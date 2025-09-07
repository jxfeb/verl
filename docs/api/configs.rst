Configuration Dataclasses
=============================

Last updated: 09/07/2025 (API docstrings are auto-generated).

This page documents commonly used configuration dataclasses for workers and engines.

Model
---------

.. automodule:: verl.workers.config.model
   :no-members:

.. autoclass:: verl.workers.config.model.HFModelConfig
   :members: __post_init__, get_processor

Engine
---------

.. automodule:: verl.workers.config.engine
   :no-members:

.. autoclass:: verl.workers.config.engine.FSDPEngineConfig
   :members:

.. autoclass:: verl.workers.config.engine.McoreEngineConfig
   :members:

Actor
---------

.. automodule:: verl.workers.config.actor
   :no-members:

.. autoclass:: verl.workers.config.actor.ActorConfig
   :members:

.. autoclass:: verl.workers.config.actor.FSDPActorConfig
   :members:

.. autoclass:: verl.workers.config.actor.McoreActorConfig
   :members:

Critic
---------

.. automodule:: verl.workers.config.critic
   :no-members:

.. autoclass:: verl.workers.config.critic.CriticConfig
   :members:

.. autoclass:: verl.workers.config.critic.FSDPCriticConfig
   :members:

.. autoclass:: verl.workers.config.critic.McoreCriticConfig
   :members:

Rollout
---------

.. automodule:: verl.workers.config.rollout
   :no-members:

.. autoclass:: verl.workers.config.rollout.RolloutConfig
   :members:

Optimizer
-----------

.. automodule:: verl.workers.config.optimizer
   :no-members:

.. autoclass:: verl.workers.config.optimizer.FSDPOptimizerConfig
   :members:

.. autoclass:: verl.workers.config.optimizer.McoreOptimizerConfig
   :members:

Reward Model
---------------

.. automodule:: verl.workers.config.reward_model
   :no-members:

.. autoclass:: verl.workers.config.reward_model.RewardModelConfig
   :members:
