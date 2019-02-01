# New PM metric based on EBM

Notice: We are still deciding on naming of these new metrics!

We have added new PM metrics:
* `ebm_duration_seconds` (summary), i.e. consists of two metrics:
    * `ebm_duration_seconds_sum`
    * `ebm_duration_seconds_count`

* `ebm_durationless_count` (counter)

`ebm_duration_seconds` measures total duration and number of EBM events.
`ebm_durationless_count` measures the number of EBM events that don't include a duration (including them in `ebm_duration_seconds_count` would have skewed the statistics).

Both metrics are segmented using two labels: `id` and `result`.

`id` can be any of the values seen in "EBM Events and Parameters" -> "EVENT_ID", as of now:

* ATTACH
* ACTIVATE
* RAU
* ISRAU
* DEACTIVATE
* L_ATTACH
* L_DETACH
* L_HANDOVER
* L_TAU
* L_DEDICATED_BEARER_ACTIVATE
* L_DEDICATED_BEARER_DEACTIVATE
* L_PDN_CONNECT
* L_PDN_DISCONNECT
* L_SERVICE_REQUEST
* DETACH
* SERVICE_REQUEST
* L_BEARER_MODIFY
* L_CDMA2000
* EXIT_PSM
* L_CONNECTION_RESUME

`result` can be any of the values seen in "EBM Events and Parameters" -> "EVENT_RESULT", which we dont' expect will change:

* Success
* Reject
* Abort
* Ignore

See last two slides of https://pdupc-confluence.mo.sw.ericsson.se/display/PCCPC/Demos+190131?preview=/69538721/69538777/Hawk%20Demo%2020190131.pptx


# New PM metric for Mnesia

We have added new metrics exposing some system info from Mnesia:

* sgsn_mme_mnesia_held_locks
    * Number of held locks.
    * gauge
* sgsn_mme_mnesia_lock_queue
    * Number of transactions waiting for a lock.
    * gauge

* sgsn_mme_mnesia_transaction_participants
    * Number of participant transactions.
    * gauge
* sgsn_mme_mnesia_transaction_coordinators
    * Number of coordinator transactions.
    * gauge
* sgsn_mme_mnesia_failed_transactions
    * Number of failed (i.e. aborted) transactions.
    * counter
* sgsn_mme_mnesia_committed_transactions
    * Number of committed transactions.
    * counter
* sgsn_mme_mnesia_logged_transactions
    * Number of transactions logged.
    * counter
* sgsn_mme_mnesia_restarted_transactions
    * Total number of transaction restarts.
    * counter

# New PM metric for Erlang VM

We have added new metrics exposing some system info about the Erlang VM:

* sgsn_mme_erlang_vm_atom_bytes_total
    * The total amount of memory currently allocated for atoms.
    This memory is part of the memory presented as system memory.
    * gauge
    * labels: 
        * usage: free, used
* sgsn_mme_erlang_vm_bytes_total
    * The total amount of memory currently allocated.
      This is the same as the sum of the memory size for processes and system.
    * gauge
    * labels:
        * kind: system, processes
* sgsn_mme_erlang_vm_dets_tables
    * Erlang VM DETS Tables count.
    * gauge
* sgsn_mme_erlang_vm_ets_tables
    * Erlang VM ETS Tables count.
    * gauge
* sgsn_mme_erlang_vm_processes_bytes_total
    * The total amount of memory currently allocated for the Erlang processes.
    * gauge
    * labels:
        * usage: used, free
* sgsn_mme_erlang_vm_system_bytes_total
    * The total amount of memory currently allocated for the emulator that is
    not directly related to any Erlang process. Memory presented as processes
    is not included in this memory.
    * gauge
    * labels:
        * usage: atom, binary, code, ets, other
