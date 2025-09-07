Workers
=================

Last updated: 09/07/2025 (API docstrings are auto-generated).

This page documents the worker components that run distributed compute for actor, critic, reference policy, and reward model under different backends.

FSDP Workers
-----------------

.. automodule:: verl.workers.fsdp_workers
   :no-members:

.. autoclass:: verl.workers.fsdp_workers.ActorRolloutRefWorker
   :members: __init__, init_model, generate_sequences, compute_log_prob, compute_ref_log_prob, update_actor, save_checkpoint, load_checkpoint

.. autoclass:: verl.workers.fsdp_workers.CriticWorker
   :members: __init__, init_model, compute_values, update_critic, save_checkpoint, load_checkpoint

.. autoclass:: verl.workers.fsdp_workers.RewardModelWorker
   :members: __init__, init_model, compute_rm_score

Megatron Workers
---------------------

.. automodule:: verl.workers.megatron_workers
   :no-members:

.. autoclass:: verl.workers.megatron_workers.ActorRolloutRefWorker
   :members: __init__, init_model, generate_sequences, compute_log_prob, compute_ref_log_prob, update_actor, save_checkpoint, load_checkpoint

.. autoclass:: verl.workers.megatron_workers.CriticWorker
   :members: __init__, init_model, compute_values, update_critic, save_checkpoint, load_checkpoint

.. autoclass:: verl.workers.megatron_workers.RewardModelWorker
   :members: __init__, init_model, compute_rm_score

Usage examples
-----------------

Minimal FSDP actor/rollout invocation (sync):

.. code-block:: python

   from omegaconf import OmegaConf
   from verl.single_controller.ray.base import create_colocated_worker_cls
   from verl.single_controller.ray import RayWorkerGroup
   from verl.workers.fsdp_workers import ActorRolloutRefWorker

   # Simplified config; see examples/config for full options
   cfg = OmegaConf.create({
       "actor": {"fsdp_config": {"fsdp_size": 1}, "ppo_mini_batch_size": 1},
       "rollout": {"name": "hf", "mode": "sync", "n": 1, "tensor_model_parallel_size": 1},
       "model": {"path": "TinyLlama/TinyLlama-1.1B-Chat-v1.0", "fsdp_config": {"wrap_policy": {}}}
   })

   worker_cls = create_colocated_worker_cls({
       "actor_rollout": (ActorRolloutRefWorker, {"config": cfg, "role": "actor_rollout"})
   })
   wg = RayWorkerGroup(resource_pool=None, ray_cls_with_init=worker_cls, device_name="cuda")
   wg = wg.spawn(prefix_set={"actor_rollout"})["actor_rollout"]
   wg.init_model()
   # prompts must be a DataProto with input tensors; see DataProto examples
   # outputs = wg.generate_sequences(prompts)

