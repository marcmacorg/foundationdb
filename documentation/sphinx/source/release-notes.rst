#############
Release Notes
#############

6.2.0
=====

Features
--------

Performance
-----------

Fixes
-----

* During an upgrade, the multi-version client now persists database default options and transaction options that aren't reset on retry (e.g. transaction timeout). In order for these options to function correctly during an upgrade, a 6.2 or later client should be used as the primary client. `(PR #1767) <https://github.com/apple/foundationdb/pull/1767>`_.
* If a cluster is upgraded during an ``onError`` call, the cluster could return a ``cluster_version_changed`` error. `(PR #1734) <https://github.com/apple/foundationdb/pull/1734>`_.

Status
------

* Added ``run_loop_busy`` to the ``processes`` section to record the fraction of time the run loop is busy. `(PR #1760) <https://github.com/apple/foundationdb/pull/1760>`_.
* Added ``cluster.page_cache`` section to status. In this section, added two new statistics ``storage_hit_rate`` and ``log_hit_rate`` that indicate the fraction of recent page reads that were served by cache. `(PR #1823) <https://github.com/apple/foundationdb/pull/1823>`_.
* Added transaction start counts by priority to ``cluster.workload.transactions``. The new counters are named ``started_immediate_priority``, ``started_default_priority``, and ``started_batch_priority``. `(PR #1836) <https://github.com/apple/foundationdb/pull/1836>`_.
* Remove ``cluster.datacenter_version_difference`` and replace it with ``cluster.datacenter_lag`` that has subfields ``versions`` and ``seconds``. `(PR #1800) <https://github.com/apple/foundationdb/pull/1800>`_.

Bindings
--------

* Go: The Go bindings now require Go version 1.11 or later.
* Go: Fix issue with finalizers running too early that could lead to undefined behavior. `(PR #1451) <https://github.com/apple/foundationdb/pull/1451>`_.
* Added transaction option to control the field length of keys and values in debug transaction logging in order to avoid truncation. `(PR #1844) <https://github.com/apple/foundationdb/pull/1844>`_.

Other Changes
-------------

Earlier release notes
---------------------
* :doc:`6.1 (API Version 610) </old-release-notes/release-notes-610>`
* :doc:`6.0 (API Version 600) </old-release-notes/release-notes-600>`
* :doc:`5.2 (API Version 520) </old-release-notes/release-notes-520>`
* :doc:`5.1 (API Version 510) </old-release-notes/release-notes-510>`
* :doc:`5.0 (API Version 500) </old-release-notes/release-notes-500>`
* :doc:`4.6 (API Version 460) </old-release-notes/release-notes-460>`
* :doc:`4.5 (API Version 450) </old-release-notes/release-notes-450>`
* :doc:`4.4 (API Version 440) </old-release-notes/release-notes-440>`
* :doc:`4.3 (API Version 430) </old-release-notes/release-notes-430>`
* :doc:`4.2 (API Version 420) </old-release-notes/release-notes-420>`
* :doc:`4.1 (API Version 410) </old-release-notes/release-notes-410>`
* :doc:`4.0 (API Version 400) </old-release-notes/release-notes-400>`
* :doc:`3.0 (API Version 300) </old-release-notes/release-notes-300>`
* :doc:`2.0 (API Version 200) </old-release-notes/release-notes-200>`
* :doc:`1.0 (API Version 100) </old-release-notes/release-notes-100>`
* :doc:`Beta 3 (API Version 23) </old-release-notes/release-notes-023>`
* :doc:`Beta 2 (API Version 22) </old-release-notes/release-notes-022>`
* :doc:`Beta 1 (API Version 21) </old-release-notes/release-notes-021>`
* :doc:`Alpha 6 (API Version 16) </old-release-notes/release-notes-016>`
* :doc:`Alpha 5 (API Version 14) </old-release-notes/release-notes-014>`
