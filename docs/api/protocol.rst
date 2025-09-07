Protocol
=================

Last updated: 09/07/2025 (API docstrings are auto-generated).

This page covers `verl.protocol` utilities for `DataProto` manipulation and helpers.

Core APIs
-----------------

.. automodule:: verl.protocol
   :no-members:

.. autofunction:: verl.protocol.pad_dataproto_to_divisor
.. autofunction:: verl.protocol.unpad_dataproto
.. autofunction:: verl.protocol.all_gather_data_proto

Examples
-----------------

.. code-block:: python

   from verl.protocol import pad_dataproto_to_divisor, unpad_dataproto
   padded, pad = pad_dataproto_to_divisor(dp, size_divisor=8)
   dp = unpad_dataproto(padded, pad)
