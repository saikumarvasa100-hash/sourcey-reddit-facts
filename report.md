# Registry fact for a Reddit answer — delivery report

> **State: draft, answer not yet posted.** The `thread` and `answer` blocks in
> `evidence.json` are null on purpose. Fill them from the real comment, re-run
> preflight, and only then deliver. Nothing below claims an answer exists.

- **What is being delivered:** one Reddit answer on a live thread, carrying a single dated fact read from the Sourcey startup-credits registry plus the public URL it came from. Registry: `https://sourcey.com/startup-credits.json`.
- **Registry state at packet build:** HTTP 200, `release_id` `sha256:8d9ba2527849990d7378f4cf0a1241a759dfca1bd3af9b486a7fd6bfb5f5e3ac`, `policy_as_of` `2026-10-05T00:00:00Z`, **589 companies and 651 offers**, with every company record carrying at least one offer.
- **Second surface:** the agent-readiness release (`https://sourcey.com/agent-readiness.json`) shares the same `release_id` and carries **106 profiles, all `lifecycle: active`**, so one digest citation covers both files.
- **The dated delta:** a previous citation of the same open file on 2026-10-30 recorded **586 companies and 648 offers**; the release has grown by **3 companies and 3 offers** since. That change is the interesting, checkable part of the fact, because it shows the registry is maintained rather than a static list.
- **How the numbers were produced:** `curl -sSL` on the two dataset URLs into `credits.json` and `readiness.json`, then a two-line `python3` count over `d["companies"]` and `sum(len(c.get("offers") or []))`. The exact commands are in `observations[kind=verification_commands]`; a reviewer can rerun them and get the same integers while that release is live.
- **Thread selection, still open:** the target must be a thread that already existed before the answer, with comments open, in a community where a registry link is on topic. Candidates are checked with a search pass and the thread itself is opened read-only before answering, so the comment is never the first thing posted on a dead or locked thread.
- **What the answer will say:** the fact, the number behind it, the release digest, the public URL, and an explicit line that the author has no affiliation with Sourcey. No affiliate links, no tracked redirects, no credentials, and no mention of any bounty — the answer has to read as a useful comment, not as an ad.
- **Known blockers, recorded rather than hidden:** no answer is posted yet, and posting needs a funded claim slot. Claiming is currently refused with `pending_review_limit` because two earlier delivered claims are still unjudged, so this packet is ready but not deliverable today.
- **Honesty note:** every figure above was fetched on 2026-11-04 from the live registry. Where something is not yet true — the thread URL, the comment URL, the posted timestamp — the field is null and labelled pending instead of being filled with a plausible value.
