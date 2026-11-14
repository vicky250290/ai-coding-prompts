# Test

The most common mistake: pointing the model at finished code and saying "write tests for this". It writes tests asserting your code does exactly what it does now, **bugs included**, and you get a green badge that locks the bug in.

## Tests from the spec, not the code

```text
Write tests for [function] from these rules — do not look at my
implementation. [rules]. Include boundary cases at [boundaries] with
hardcoded expected values.
```

A filled-in example:

```text
Write tests for calculateRefund. Here are the business rules — do not
look at my implementation.
- Full refund if cancelled more than 7 days before the event
- 50% between 7 days and 24 hours
- Nothing within 24 hours
- The 2% processing fee is never refunded
- Refunding an already-refunded booking throws AlreadyRefundedError
Include boundary cases at exactly 7 days and exactly 24 hours,
with hardcoded expected values.
```

**"Hardcoded expected values" matters.** A test that computes the expected number with the same formula as your code is running your bug twice and checking the results match.

## Find coverage gaps

```text
Here's the function and my existing tests. Which branches and input
classes are untested?
```

## Before you trust a suite

- **Sabotage it:** flip a comparison operator on purpose. If nothing goes red, the tests are decoration.
- **Read the assertions:** `expect(save).toHaveBeenCalled()` tells you far less than `expect(saved.amount).toBe(4750)`.
