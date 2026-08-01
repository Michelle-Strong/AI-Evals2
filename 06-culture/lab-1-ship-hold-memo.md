# Final Recommendation: Ship / Hold

From c9179a4cc51ae7c2a51dbe21b1b713735dc65aee Mon Sep 17 00:00:00 2001
From: Michelle Strong <michelle.strong2@hotmail.co.uk>
Date: Thu, 30 Jul 2026 18:30:02 +0000
Subject: [PATCH] M6: complete ship/hold memo - HOLD recommendation with M2-M5
 evidence

---
 06-culture/lab-1-ship-hold-memo.md | 60 +++++++++++++++++++++++-------
 1 file changed, 47 insertions(+), 13 deletions(-)

diff --git a/06-culture/lab-1-ship-hold-memo.md b/06-culture/lab-1-ship-hold-memo.md
index b992296..405bf1e 100644
--- a/06-culture/lab-1-ship-hold-memo.md
+++ b/06-culture/lab-1-ship-hold-memo.md
@@ -4,35 +4,69 @@
 >
 > The memo that ties it all together: given the evidence, do you ship, hold, or ship-with-conditions? This is your final pitch.
 
+**To:** CPO
+**From:** Michelle Strong
+
 ## Recommendation
 
-> **Decision:** _SHIP / HOLD / SHIP WITH CONDITIONS_
+> **Decision:** HOLD
+
+I recommend we HOLD Ascend IQ to enterprise customers in the next sprint, contingent on the documented mitigation plan, to protect $4.2M in at-risk renewal revenue.
+
+## 1. The Arguments
 
-_One paragraph: the decision and the single most important reason for it._
+**1. Product Integrity — the core "verified intelligence" promise is broken.**
+Ascend IQ's value proposition is trustworthy, verified answers for VP-level buyers. Right now it fabricates pricing, invents unconfirmed facts, and misrepresents competitor specs — the exact failures that make "verified" a false claim.
 
-## 1. The evidence
+**2. Business Risk — $4.2M in enterprise renewal revenue is directly exposed.**
+The hallucination failures aren't cosmetic: quoting incorrect pricing to enterprise buyers creates contract/revenue-recognition liability and reputational risk with the VP audience this product is built for.
 
-_Pull the key numbers from your eval suite and gates. Let the data carry the argument._
+**3. Eval Readiness — the gate hasn't been met, and there's no partial-credit path.**
+The pricing hallucination check is a Hard gate at a 100% threshold, and it is currently failing. Per our own governance model, this is a full pass/fail gate — there is no shadow-launch or partial-rollout option until it clears.
 
-| Metric | Result | Bar | Pass? |
+## 2. Evidence · Trust Metrics
+
+| Metric | Result | Bar (Gate) | Pass? · Source |
 |---|---|---|---|
-| _…_ | _…_ | _…_ | _…_ |
+| Pricing hallucination — code check (Layer 1) | 0 | 100% accuracy | **FAIL** · `03-eval-suites/lab-1-eval-suite.md` |
+| Pricing hallucination — LLM judge (Layer 3) | 0 | 100% accuracy | **FAIL** · `03-eval-suites/lab-1-eval-suite.md` |
+| Latency | 4.2s | 2.0s target | **FAIL** (Soft gate) · `04-eval-gates/lab-1-gate-map.md` |
+| Hallucination rate (500-item gold set) | Not yet re-tested | >99% pass | **PENDING** — blocking condition for reopen · `05-scale/lab-1-coverage-matrix.md` |
+| Bias / fairness consistency | Not yet re-tested | >95% consistency | **PENDING** — blocking condition for reopen · `05-scale/lab-1-coverage-matrix.md` |
+
+## 3. Residual risk
+
+**Ship-path risk:** Shipping now with a failing Hard gate on pricing hallucination risks quoting incorrect enterprise pricing directly to VP buyers — creating contract/revenue-recognition exposure and reputational damage with the $4.2M in renewal accounts this release is meant to protect. A single fabricated figure cited externally by a customer could turn a product bug into a legal or trust incident.
+
+**Hold-path risk:** Delaying the sprint costs us competitive window and momentum — every week Ascend IQ isn't in front of Enterprise buyers is a week a competitor's tool could be evaluated instead, and it risks eroding internal confidence that the roadmap will ship on time. This is a real but bounded cost, and it's recoverable; a mispriced quote reaching a live enterprise contract is not.
+
+**What's still uncovered after the Hard gate clears:** Toxicity has no validated detection instrument yet (flagged as a critical gap in the M5 coverage matrix), and latency is an accepted gap not yet remediated. Neither blocks this HOLD decision, but both should be tracked post-mitigation.
+
+## 4. Conditions to reopen
+
+The following must be true before Ascend IQ ships to enterprise customers:
 
-## 2. Residual risk
+- **Pricing hallucination gate passes at 100%** — both the Layer 1 code-based $ comparison against the live pricing API and the Layer 3 LLM judge, re-run against the full trajectory test set with zero exceptions (per `03-eval-suites/lab-2-eval-spec.md` acceptance criteria).
+- **Hard-verification gate live in production:** no dollar figure is returned to a user unless it is confirmed against the live pricing API in real time; if unverifiable, the agent declines and routes to the verified source page.
+- **Hallucination rate re-tested** against the 500-item gold set at >99% pass, and **bias/fairness re-tested** at >95% consistency — both currently pending, per `05-scale/lab-1-coverage-matrix.md`.
+- **Sign-off obtained** from Group PM, Eval Owner, and Engineering Lead, per the Eng ticket acceptance criteria.
 
-_What still isn't covered? What could go wrong after launch, and how would you know?_
+**Monitored post-launch:** every pricing claim logged with source, timestamp, and confidence; in-product "flag this figure" feedback affordance live on all data-bearing responses to catch drift or edge cases the eval suite didn't anticipate.
 
-## 3. Conditions (if "ship with conditions")
+## 5. Next Step
 
-_What must be true to ship, and what's monitored after?_
+**Decision needed from the CPO by August 1:**
+1. Approve the HOLD on Ascend IQ's enterprise release for the next sprint.
+2. Approve resourcing for the remediation team to close the pricing hallucination gate (hard-verification gate + regression re-run).
+3. Go/no-go review on **August 1** based on the reopen conditions above — a revised go-live date for the Top 50 Enterprise cohort will be proposed at that review if the gate passes.
 
-## 4. The pitch
+## 6. The pitch
 
 _3 to 5 sentences you'd say to a VP to get a ship/hold decision. Confident, evidence-led, honest about risk._
 
-## 5. What I learned
+## 7. What I learned
 
-_The biggest shift in how you think about evaluating AI products from this certification._
+The real shift for me was continuing to ensure I framed the business outcomes alongside the metrics. It's not enough to know a gate failed at 0% against a 100% threshold — what makes that number matter to a CPO is tying it directly to the $4.2M in at-risk renewal revenue and the reputational exposure with the exact VP audience the product is built for. Defining "good enough" meant refusing to let a passing eval stand on its own as the argument; the metric only earns its weight in the room once it's connected to what it actually costs or protects for the business.
 
 ## Link to final deck
 
-- 
2.43.0

> Module 6 · Culture · repo file; becomes the Ship/Hold slide of your final pitch deck
>
> The memo that ties it all together: given the evidence, do you ship, hold, or ship-with-conditions? This is your final pitch.

## Recommendation

> **Decision:** _SHIP / HOLD / SHIP WITH CONDITIONS_

_One paragraph: the decision and the single most important reason for it._

## 1. The evidence

_Pull the key numbers from your eval suite and gates. Let the data carry the argument._

| Metric | Result | Bar | Pass? |
|---|---|---|---|
| _…_ | _…_ | _…_ | _…_ |

## 2. Residual risk

_What still isn't covered? What could go wrong after launch, and how would you know?_

## 3. Conditions (if "ship with conditions")

_What must be true to ship, and what's monitored after?_

## 4. The pitch

_3 to 5 sentences you'd say to a VP to get a ship/hold decision. Confident, evidence-led, honest about risk._

## 5. What I learned

_The biggest shift in how you think about evaluating AI products from this certification._

## Link to final deck

_[link]_
