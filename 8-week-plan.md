# Staff Backend Engineer — 8-Week Prep Plan

**Target:** Staff Software Engineer / Staff Backend Engineer
**Baseline:** ~12 yrs, strong Java/Spring Boot/REST/microservices/DB/cloud
**Budget:** 10 hrs/week → **6h System Design · 2.5h DSA · 1.5h Staff skills**
**Total:** 80 hrs (48h SD · 20h DSA · 12h Staff)

---

## Guiding principles (read once, then don't re-litigate)

1. **System Design is the boss level.** At Staff, they're not testing whether you
   *know* Kafka — they assume you do. They test whether you can reason about
   tradeoffs, failure modes, and evolution under ambiguity. Every SD week ends
   with you *writing or speaking* a design, not just reading about one.
2. **DSA is maintenance, not the main quest.** You're not a new grad. Goal =
   pattern fluency so you never freeze, not 500 LeetCode problems. Quality > grind.
3. **Staff ≠ Senior + more code.** The 1.5h/week track is about scope, influence,
   and written communication. It compounds. Don't skip it because it feels "soft."
4. **Anchor everything to your real systems.** You have GTA / timesheet-service /
   Kafka / Cosmos / Redis / PingFed in your day job. Use them as living case
   studies — it makes the abstract concrete AND builds promo-packet ammo.
5. **Each week builds on the last.** Don't reorder. Week N assumes Week N-1.

---

## The Arc at a Glance

| Wk | System Design (6h)                         | DSA (2.5h)                  | Staff (1.5h)                       |
|----|--------------------------------------------|-----------------------------|------------------------------------|
| 1  | Fundamentals & estimation                  | Arrays/strings/hashing      | Staff archetypes & scope           |
| 2  | Storage: SQL/NoSQL, indexing, sharding     | Two pointers / sliding win. | Writing: design docs / RFCs        |
| 3  | Caching, LB, consistent hashing, CDN       | Trees & recursion           | Technical strategy & vision        |
| 4  | Async, messaging, Kafka, event-driven      | Graphs (BFS/DFS)            | Influence without authority        |
| 5  | API design, rate limiting, idempotency + **Design #1** | Heaps / intervals / greedy | Driving alignment & tradeoffs |
| 6  | Distributed consistency: txns, sagas, consensus | Dynamic programming    | Mentorship & sponsorship           |
| 7  | **Mock designs** (2 full end-to-end)       | Backtracking / tries        | Execution: scoping & risk          |
| 8  | Reliability/observability + **Capstone**   | Mixed mock + weak spots     | Promo packet & behavioral          |

---

## WEEK 1 — Foundations: speak the language of scale

**System Design (6h)**
- (2h) Back-of-the-envelope estimation. Memorize the "latency numbers every
  engineer should know," QPS math, storage math, bandwidth math. Do 5 estimation
  drills (e.g. "how much storage for 1B users × 2KB profile?").
- (2h) Core theory: CAP (and why it's oversimplified), PACELC, consistency
  models (strong / eventual / causal / read-your-writes), availability vs
  durability, SLA/SLO/SLI + error budgets.
- (2h) The building-blocks map: LB, app tier, cache, DB, queue, blob store, CDN.
  Sketch the "generic web-scale architecture" from memory 3× until it's muscle.
- **Deliverable:** a one-page cheat sheet of latency numbers + estimation formulas.

**DSA (2.5h)** — Arrays, strings, hashing. 6–8 problems. Patterns: frequency maps,
in-place manipulation, hashset dedup. (e.g. Two Sum, Group Anagrams, Longest
Consecutive Sequence.)

**Staff (1.5h)** — Read *StaffEng.com* archetypes (Tech Lead, Architect, Solver,
Right Hand). Write 3 paragraphs: which archetype fits you today, which you're
growing into, and 2 examples from your current work (GTA backfill is a great one).

---

## WEEK 2 — Storage & data modeling (the part most people fake)

Builds on W1: now you can estimate, so you can choose storage intelligently.

**System Design (6h)**
- (2h) SQL vs NoSQL *decision framework* — access patterns first, not hype.
  Document/KV/wide-column/graph/time-series and when each wins.
- (2h) Indexing internals: B-tree vs LSM-tree (why Cassandra/RocksDB use LSM),
  write vs read amplification, covering indexes, composite index ordering.
- (2h) Partitioning/sharding (range vs hash vs directory), replication
  (leader-follower, multi-leader, leaderless/quorum), hotspots, rebalancing.
- **Deliverable:** Reverse-engineer your **Cosmos** tracking container — write up
  its partition key choice, why, and what breaks at 100× scale.

**DSA (2.5h)** — Two pointers + sliding window intro. 6–8 problems (Valid
Palindrome, Container With Most Water, 3Sum, Longest Substring Without Repeats).

**Staff (1.5h)** — Read Google's design-doc culture / a good RFC template. Start a
**personal design-doc template** you'll reuse (Context → Goals/Non-goals →
Options → Decision → Risks → Rollout).

---

## WEEK 3 — Caching, load balancing, and the distribution primitives

Builds on W2: you have data stores; now make them fast and spread the load.

**System Design (6h)**
- (2h) Caching strategies: cache-aside vs read/write-through vs write-behind,
  TTL/eviction (LRU/LFU), thundering herd, cache stampede, invalidation
  ("one of the two hard problems"). Map this onto your **Redis** usage.
- (2h) Consistent hashing (deep — draw the ring, virtual nodes, why it beats
  mod-N). This unlocks sharding, caches, and Kafka partition intuition.
- (2h) Load balancing (L4 vs L7, algorithms, health checks, sticky sessions) +
  CDN + edge caching.
- **Deliverable:** Design a distributed cache tier for a read-heavy service;
  justify eviction + invalidation + failure behavior.

**DSA (2.5h)** — Trees & recursion. 6–8 problems (traversals, max depth, LCA,
validate BST, level-order). Nail recursive→iterative conversions.

**Staff (1.5h)** — Technical strategy: read on "technical vision" and 6-pager
thinking. Draft a half-page vision for one messy area you own at Walmart.

---

## WEEK 4 — Async, messaging & event-driven architecture

Builds on W3: synchronous scaling has limits; go async.

**System Design (6h)**
- (2h) Message queues vs logs vs pub/sub. Delivery semantics (at-most/at-least/
  exactly-once — and why exactly-once is a lie you engineer around with
  idempotency). Ordering, backpressure, DLQs.
- (2h) **Kafka deep dive** (your home turf, go deeper): partitions & keys,
  consumer groups, rebalancing, offsets, retention/compaction, ISR, exactly-once
  semantics/transactions. Understand *why*, not just config.
- (2h) Event-driven patterns: event sourcing, CQRS, outbox pattern, choreography
  vs orchestration. Their failure modes and debugging pain.
- **Deliverable:** Redesign a currently-synchronous flow you own as event-driven;
  list what gets better AND what gets harder (eventual consistency, ordering).

**DSA (2.5h)** — Graphs. 6–8 problems (BFS/DFS, number of islands, clone graph,
course schedule/topological sort). Learn adjacency-list muscle memory.

**Staff (1.5h)** — Influence without authority. Read on driving decisions across
teams. Write up one time you changed a technical direction you didn't own.

---

## WEEK 5 — Putting it together: APIs, protection, and your FIRST full design

Builds on W1–W4: you now have all primitives. Time to design end-to-end.

**System Design (6h)**
- (1.5h) API design at scale: REST vs gRPC vs GraphQL, versioning, pagination,
  idempotency keys, API gateway responsibilities.
- (1.5h) Protection patterns: rate limiting (token bucket / leaky bucket /
  sliding window), throttling, circuit breakers, bulkheads, retries + jitter.
  (You literally hit `@Size(max=5000)` + 429 handling in GTA — perfect case.)
- (3h) **Full Design #1: Design a URL shortener OR a rate limiter.** Do the whole
  ritual: requirements → estimation → API → data model → high-level → deep-dive
  on 1 component → bottlenecks → tradeoffs. Time-box to 45 min, then critique
  your own answer for 15.
- **Deliverable:** Written design doc for Design #1 using your W2 template.

**DSA (2.5h)** — Heaps, intervals, greedy. (Merge Intervals, Meeting Rooms II,
Kth Largest, Top K Frequent, Task Scheduler.)

**Staff (1.5h)** — Driving alignment: RFC review etiquette, disagree-and-commit,
making reversible vs irreversible ("one-way door") decisions explicit.

---

## WEEK 6 — Distributed consistency & the hard theory

Builds on W5: your designs work on the happy path; now handle correctness under
partition and concurrency.

**System Design (6h)**
- (2h) Distributed transactions: 2PC (and why people avoid it), **saga pattern**
  (orchestration vs choreography), compensating transactions, idempotency as the
  backbone. (Your chunked-backfill retry logic *is* an idempotency case study.)
- (2h) Consensus: Raft (leader election, log replication) at an intuition level,
  a nod to Paxos, quorums (R+W>N), read-repair, hinted handoff. Where ZooKeeper/
  etcd fit.
- (2h) Advanced consistency: vector clocks, CRDTs, conflict resolution,
  linearizability vs serializability (know the difference cold — it's a common
  Staff-level gotcha).
- **Deliverable:** Take one design and write its "consistency & failure model"
  section: what happens on node loss, network partition, duplicate delivery.

**DSA (2.5h)** — Dynamic programming (the one to actually practice). 1D → 2D.
(Climbing Stairs, House Robber, Coin Change, LIS, Edit Distance, 0/1 Knapsack.)
Learn to spot "choices + overlapping subproblems."

**Staff (1.5h)** — Mentorship & sponsorship: difference between the two, how to
scale yourself, reviewing others' designs as a force multiplier. Identify 1 person
you can actively sponsor.

---

## WEEK 7 — Mock interviews: perform under time pressure

Builds on everything. This week is *reps*, not new theory.

**System Design (6h)**
- (3h) **Mock #1 — Design a news feed / activity feed** (fan-out on write vs read,
  hot users, ranking, pagination). Full ritual, 45 min timed + 15 min self-review.
- (3h) **Mock #2 — Design a distributed job scheduler / notification system**
  (deliberately close to your GTA kubie-jobs world so you can go deep). Timed +
  reviewed. If possible, do at least one of these with a peer or record yourself.
- **Deliverable:** A "mistakes I made" list from both mocks. Turn each into a
  checklist item.

**DSA (2.5h)** — Backtracking + tries. (Subsets, Permutations, Combination Sum,
Word Search, Implement Trie, Word Search II.)

**Staff (1.5h)** — Execution: project scoping, breaking epics into milestones,
identifying risk early, writing a crisp status update. Draft one for a real project.

---

## WEEK 8 — Reliability, capstone & the promo/interview package

Builds on W7: polish, cover the "senior-plus" topics, and package your narrative.

**System Design (6h)**
- (2h) Reliability & operability: observability (logs/metrics/traces), the
  four golden signals, SLOs/error budgets, graceful degradation, load shedding,
  chaos/failure testing, multi-region & disaster recovery, blue-green/canary.
- (1h) Security & multi-tenancy basics: authn/authz (you've got PingFed/OAuth),
  secrets, data isolation, rate-limit-as-defense.
- (3h) **Capstone: Design a large-scale system of your choice** end-to-end
  (e.g. "Design Uber," "Design a payments ledger," or a scaled-up version of a
  Walmart system you own). This is your dress rehearsal — cover estimation,
  data, scale, consistency, failure, ops. 60 min, then a brutal self-review.
- **Deliverable:** Polished capstone doc = your best writing sample.

**DSA (2.5h)** — Mixed timed set + revisit your 2 weakest patterns from earlier
weeks. No new material; consolidate.

**Staff (1.5h)** — **Promo packet + behavioral prep.** Build a "brag doc" of
Staff-level impact (scope, influence, ambiguity you resolved — GTA backfill root
cause + chunking redesign is a textbook Staff story). Prep STAR answers for:
biggest technical decision, cross-team conflict, mentoring, a failure you owned.

---

## How to actually stay on track

- **Weekly ritual:** end each week by writing a 3-bullet "what clicked / what's
  fuzzy / what to revisit." Fuzzy items get 15 min at the start of next week.
- **Don't read passively.** Every SD hour should end with *you producing* — a
  sketch, a doc section, or a spoken walkthrough. Reading ≠ learning at Staff level.
- **Resources (pick, don't hoard):** DDIA (*Designing Data-Intensive Applications*)
  as your SD spine — 1 chapter/week roughly maps to this plan; *System Design
  Interview* (Alex Xu) Vols 1–2 for the ritual/mocks; StaffEng.com + *The Staff
  Engineer's Path* (Tanya Reilly) for the 1.5h track; NeetCode 150 for DSA patterns.
- **Interview logistics:** by Week 5 start doing designs out loud, ideally with a
  peer. Talking is a separate skill from knowing.

---

### Fast reference: total time invested
- System Design: 48h (60%) ← primary focus 
- DSA: 20h (25%)
- Staff skills: 12h (15%)
