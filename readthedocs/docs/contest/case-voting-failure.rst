================================================================================
Voting Failure
================================================================================

.. toctree::
   :maxdepth: 1


   /docs/contest/case-voting-failure-over-blocking-number.rst
   /docs/contest/case-voting-failure-under-blocking-number.rst
   /docs/contest/case-voting-failure-proposing.rst
   /docs/contest/case-voting-failure-sign-accept.rst

.. note::
    .. glossary::
        *blocking number*

            In voting, to reach a majority for YES, the YES ballots must be over
            threshold. *blocking number* is the minimum number to prevent to reach the majority. For example,

                * there are 4 total voters,
                * threshold for majority is 3,

            At this condition, *blocking number* is 2. Simply to say,

            .. code-block:: none

                blocking number = <voters> - <threshold> + 1
