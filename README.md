# Support Engineering Work Samples

Write-ups from real support and debugging work at StrategyForge, a broker-integrated
trading journal. Trades import from brokerage accounts through SnapTrade, an API
aggregator, and most of the interesting problems live in that pipeline.

These are the actual investigations, including the wrong turns. Every log line, API
response and code snippet is real.

---

### [Debugging a Silent Data Corruption Bug in a Broker API Integration](fractional-quantities-corrupting-pnl.pdf)

A crypto trade worth $11.37 was reporting a profit of $8,241.71.

Three separate defects across the database, the profit calculation and five import paths,
each one hiding the next. Found by reading the raw API payload rather than the vendor's
documentation, which describes what fields can exist but not what a broker actually sends.
Fixing it surfaced two more bugs that had been concealing each other.

### [Finding an API Integration Bug That Reported Success](date-range-that-fetched-the-wrong-period.pdf)

A sync for May returned trades from August.

No error, and the imported trades were real, just from a period nobody asked for. Found by
opening the vendor's own API request log, which showed we were sending a day count instead
of the dates the user picked. Invisible in our code and invisible in our database. A third
bug turned up in the fix itself, caught by a test before it shipped.

### [Debugging an API Integration at StrategyForge](debugging-a-silent-api-integration-bug.pdf)

Every trade in a user's history showed the same account balance, and it was the wrong
number.

Every API call returned 200 OK. Nothing failed. A healthy pipeline was confidently
producing wrong data. The obvious one-line fix would have solved half the complaint and
sent the user straight back.

### [QA Test Cases for API Feature Testing](QA%20Test%20Cases.jpg)

Test cases written for broker import features, covering the edge cases that actually break
integrations: partial fills, fractional quantities, timezone boundaries and repeat syncs.

---

## The thread running through these

Every one was found by reading what the system actually produced. Raw payloads, request
logs, type definitions. Not by reading documentation and assuming it matched reality, and
not by guessing from the symptom.

Several were found because a first explanation turned out to be wrong and got checked
anyway.

---

**Trent Dozier** · [linkedin.com/in/doziertrent](https://linkedin.com/in/doziertrent) · trentmdozier@gmail.com

*Account identifiers removed from all logs and API responses.*
