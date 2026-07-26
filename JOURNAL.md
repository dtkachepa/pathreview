## Week 7 – Issue selection

**Issue link:** [https://github.com/ascherj/pathreview/issues/153]

**Issue title:** Faithfulness checker crashes when a context chunk has `text: None`

**Tier:** [x] Tier 1  [ ] Tier 2  [ ] Tier 3

**Problem summary:**

The faithfulness checker crashes when a retrieved context chunk contains `None` instead of text. The crash occurs because the checker passes the null value into `join()`, which only accepts strings. A successful fix should handle null values safely while keeping the existing behavior for valid context chunks. The affected code is located in `rag/evaluator/faithfulness_checker.py`.

**Issue-selection reasoning:**

I can explain the problem and expected behavior clearly:
- the faithfulness checker should return a score rather than crash when a context chunk contains `text: None`. 
I located the affected `check()` method in `rag/evaluator/faithfulness_checker.py` and reviewed the related test in `tests/unit/test_faithfulness_checker.py`.
This is my first open source contribution whch is why I chose this Tier 1 issue. 
I checked the issue comments and cohort ledger and am comfortable with the number of existing claims. I found no unresolved blockers or dependencies, and I estimate that the investigation, implementation, and testing can be completed before the Week 9 deadline.

**Branch name:** `fix/153-handle-none-context-text`

**Setup confirmation:** [y] App runs locally at `localhost:5173`

**Cohort ledger:** [y] Issue added to cohort ledger

## Week 8 – Reproduction & solution planning

**Reproduction commit link:** [https://github.com/dtkachepa/pathreview/tree/fix/153-handle-none-context-text]

**Reproduction summary:**

I ran the existing `test_none_context_chunk_text` test with a context chunk containing
`{"text": None}`, and it failed with the confirmed
`TypeError: sequence item 0: expected str instance, NoneType found` at the `" ".join(...)`
operation in `rag/evaluator/faithfulness_checker.py`.

Exact focused command used to reproduce it:

```
python -m pytest tests/unit/test_faithfulness_checker.py::TestFaithfulnessChecker::test_none_context_chunk_text -q
```

**PLAN.md link:** [https://github.com/dtkachepa/pathreview/blob/fix/153-handle-none-context-text/PLAN.md]

**Blockers or open questions:**
No blockers or open questions