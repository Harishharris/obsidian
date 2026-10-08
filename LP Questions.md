1. Tell me about a time when you had to implement something challenging (sotioneapps)
		Explain what sotioneapps is and being new to the team, and only had 1 month time to complete all of these and had to drop the soti search feature
---
1. Tell me about a time when you had recieved critical feedback and how worked upon it.
		So i received critical feedback during the compliance review. so this compliance review is the one where once we're done with all the development, we'd give a code changes to review. the reviews that I got was very critical. part of the reason was that its written in c++ and my changes had be there and it was lacking a proper structure and since i was the one modifying the already long big 600 line method, i got "to make the ugly code uglier" and like this i got. this was coming from a senior software architect with well over 25 years at the company. so I've made all the required changes and do the refactoring as needed and got the compliance reveiw resolved.
---
1. Tell me about a time when you had to deep dive into subject matter. 
2. Tell me about a time when you didn't know how to proceed
3. Tell me about a challenging problem you solved
4. Tell me about a time you had to investigate an unfamiliar problem
5. Tell me about a time you worked independently
		**MobiControl Architecture or**
		So this was very beginning of me joining the company and I got a bug where if we sign-in using any Identity Provider and if we duplicate the tab and tries to log out, it wont. it will take us to the home page again means we cant even log out of the system. this is a very serious threat. since being new and dont have much context around the system, i had to read and understand a lot of code and make certain assumptions regarding the system and validating them to make sure i'm moving in the right path or not. in turns out that it is because of a timing issue means by the time, we try to log out, our system is detecting that we are already loged in and redirecting us to the home page. So i had added a fix to increase the timer to wait for the web socket connection to fire which is 3 seconds. this is a frontned fix. Also there was one more issue that moment we log out, it wasn't taking us to the login page. so I've added one more API to redirect us to the login page again.
------
7. Tell me about a time when you improved upon your shortcomings.
	- either identity provider bug (above one) or the compliance review one gotta decide tho
8. Tell me about a time when you missed a deadline, what could you have done better.
	- we didn't miss the deadline but there was a case where we had to deliberately make a choice to descope one of the story to avoid putting the entire delivery at risk
9. It was something like how did you know you were implementing the right solution, what you could've done better
	- key storage service
---
- Time you went above and beyond your expectations
	- SotiOneApps
----
1. A time you took on something significant outside your responsibility
2. Tell me a time where you have taken out of your responsibility.
	- So there was an epic we were doing called Key Storage Service where I was only responsible for delivering the CLI it. but i wanted to have a look at the design doc to see how the whole thing was being built. So in that design doc, I could see that they were using username and password to identity the admin instead of using the installationID and the registration code. So i've flagged it and proposed my changes and we've told the same thing in the architectural design review as well and it got approved.
---
1. Tell me something that you are not good at
	- I tend to make design assumptions upfront and build on them without explicitly validating them first. I learned this during SOTI ONE Apps when my JSON storage proposal was rejected — I had formed a strong opinion independently and the architecture team identified real problems with it. Now I explicitly document my assumptions in design docs and get them reviewed early. The MoMs I drove during SOTI ONE Apps were partly a result of that habit.
---
1. How would you learn a new Technology
	- When you joined the new team you had no familiarity with how Management Server and Deployment Server communicate. You spent one week before touching any feature code — reading the codebase, putting debuggers at key points, experimenting with the system, triggering check-ins and observing what happened at each stage. You discovered the message queue behavior wasn't in any documentation — you found it through the debugger. That understanding directly shaped your design decisions for SOTI ONE Apps.
	- Read the code first to get the structure, run it with debuggers to see actual behavior, then experiment by triggering real flows and observing what happens. Documentation tells you what the system is supposed to do. Debuggers tell you what it actually does. The gap between those two is usually where the important things are
----
1. Most Challenging Project you have ever worked on
	- SOTI One Apps project: new team; unfamiliar codebase; not enough time for Architectural Design Review, security review; unstructured data format; different timelines from agent team, app teams, etc; 
---
- Tell me a time where you worked on tight deadlines.
	- SotiOneApps
----

so there were few LPs such as customer focused pending
there are few tasks that I need which could be used for some or the other LPs
for bias for action, we can use the sotioneapps the section where we escalte the soti search to the manager

----
## 1, 2. SOTI One Apps (Ownership, Deliver Results)

**STAR:**

Situation: SOTI MobiControl manages over 25 million devices globally. SOTI has 7 in-house apps installed on managed devices but administrators had zero visibility into which of these apps were installed on which device. I had just transferred to a new team when I was handed this feature to own end to end with a one month deadline.

Task: Design and deliver the entire backend — snapshot ingestion pipeline, data processing layer, database schema, and REST API — as a new team member with no prior familiarity with the codebase or stakeholders.

Action: Rather than waiting to settle in I immediately drove the first design discussion within days of joining, documented every decision through MoMs to keep stakeholders aligned, and coordinated across the architecture team and agent team simultaneously. I added a new KV pair to the device check-in snapshot for SOTI ONE apps data and handled the unchanged-snapshot edge case by comparing incoming data against the database — our system doesn't resend unchanged snapshots for bandwidth reasons so I had to account for the case where no new snapshot arrives. On the processing side I implemented a per-app processor framework with a shared extension table and bulk MERGE upsert. When I assessed midway that integrating SOTI Search would put core delivery at risk I recommended descoping it to my manager — that was my call, not something I was told to do. Compliance review was closed and the feature shipped on time.

Result: Feature runs on every device check-in across 25 million managed devices. Administrators have full visibility into SOTI ONE app installations for the first time. Delivered within one month of joining the team, driving the entire process end to end as a new team member.

---

**Deep follow-ups and answers:**

Q: You said you were new to the team. How long had you actually been on the team before you started driving design sessions?

A: I had been on the team for just a few days. I didn't have deep familiarity with the codebase yet but I could see the deadline was fixed and waiting to get comfortable wasn't an option. I started driving the design sessions immediately.

---

Q: The descoping decision — was that ultimately your call or your manager's?

A: It was my recommendation. I assessed that SOTI Search had been added late in the scope and would require modifications across multiple touchpoints — payload changes, snapshot handling, testing — and would put the core feature at risk. I brought this to my manager with a clear recommendation to descope it. My manager agreed. The recommendation was mine.

---

Q: You said you drove MoMs. What does that actually mean — did you facilitate the meetings, write the notes, or both?

A: Both. I set the agenda for each session, facilitated the discussion, and wrote the MoMs immediately after each session so every decision was documented in writing. This was important because I was new and didn't have established trust with the stakeholders yet — written documentation meant anyone could flag disagreements before they became blockers.

---

Q: What specifically was the hardest part of owning this as someone new to the team?

A: The cross-team coordination. I needed things from the architecture team and the agent team — teams I had no existing relationship with. Getting the architecture team to review and approve my design doc, and getting the agent team to make the snapshot changes I needed, required me to move quickly on building credibility. I did that by being specific in my asks, keeping requirements narrow and well-defined, and not changing them mid-flight.

---

Q: What would have happened if you hadn't flagged the scope risk early?

A: We would have attempted all three workstreams and most likely missed the deadline or shipped something incomplete. The SOTI Search integration alone would have added significant complexity. By flagging it early we protected the core delivery which was the actual business priority — giving admins visibility into SOTI ONE apps for the first time.

---

Q: What would you do differently if you had to do this again?

A: I would push to get architecture review scheduled earlier. We lost some time waiting for the architecture team to review the design doc. If I had been more aggressive about getting that meeting on the calendar in the first week, we would have had more runway after the review.

------------

Q: You descoped SOTI Search to hit the deadline. Isn't that just delivering less than what was asked?

A: The three workstreams were not equal in priority. SOTI Search was added late in the cycle — it wasn't in the original scope. The core ask was giving administrators visibility into SOTI ONE app installations. That was delivered completely and on time. Descoping something that was added late to protect the original commitment is not delivering less — it's prioritizing correctly. Shipping the core feature well beats shipping everything poorly.

---

Q: What does "on time" mean specifically — what was the deadline and when did you actually ship?

A: The deadline was tied to the release cycle — one month from when I was assigned the task. We shipped within that window with compliance review closed before the release date.

---

Q: The API always returns all 7 apps — why is that a delivery decision rather than just a technical one?

A: It was a conscious decision that affected how the frontend team could build against the API. If the API returned only installed apps, the frontend would need to handle missing entries — checking for null, rendering placeholders, handling partial data. By always returning all 7 apps with a NotInstalled status for absent ones, I gave the frontend a consistent contract they could build against without defensive handling. That reduced their delivery risk which affected the overall feature shipping on time.

---

Q: What was the biggest risk to delivery and how did you manage it?

A: The biggest risk was the unchanged-snapshot handling. Our system doesn't resend unchanged snapshots for bandwidth reasons — this is by design for a platform managing 25 million devices. If I hadn't accounted for this correctly, the system would show stale or missing app data for devices whose snapshots hadn't changed. I solved it by comparing incoming snapshot data against the database so the system always has accurate app state regardless of whether a new snapshot arrived.

## 3. Key Storage Service (Dive Deep) - Alternate (Linux Bug), Duplicate tab logout issue

**STAR:**

Situation: SOTI was building a key storage service to isolate master encryption keys from the main database for EU compliance. During the design phase the team had an open question on authentication for the disaster recovery CLI — the most sensitive operation in the system, where an admin retrieves master encryption keys directly during a disaster.

Task: I was the CLI owner and needed to validate whether the proposed authentication scheme was correct for our specific deployment context before implementation began.

Action: The proposed scheme used username and password. I thought through how this works in on-prem enterprise environments step by step — each installation would need local user accounts, those accounts would need local management, and there was no reliable way to trace which local account belonged to which customer admin. In a break-glass scenario for master key retrieval, that accountability gap is a serious problem. I went deeper into what identifiers already existed in our system — the installationID and registration code are already unique per customer installation, already in our database, and map directly to a specific customer account. I raised this during the design review with the specific flaw identified and the alternative clearly articulated. I also designed a read-back verification step for key persistence — after writing the key, read it back by TraceId before returning 204, and store it as binary rather than string to prevent the key appearing in logs.

Result: The authentication model I proposed was adopted. The read-back verification and binary storage decisions were signed off by senior engineers. The service shipped on schedule.

---

**Deep follow-ups and answers:**

Q: How did you identify the accountability gap — did someone point it out or did you figure it out yourself?

A: I figured it out myself while reviewing the design doc. I was thinking through how the username/password scheme would actually work in an on-prem enterprise environment — specifically, who creates the local accounts, how many there would be across different installations, and how you would trace a specific access event back to a specific admin. When I mapped that out I realized there was no clean answer. That's when I identified it as a problem worth raising.

---

Q: Why read-back verification instead of just trusting the write transaction?

A: A write returning no error guarantees the operation was attempted — it doesn't guarantee the data is actually there and retrievable. For a master encryption key, those are two different guarantees and both matter. A silent persistence failure in this specific context means a customer potentially loses their master key permanently with no error surfaced. The read-back empirically verifies recoverability before we tell the caller success.

---

Q: Why store the master key as binary rather than string?

A: String representation of sensitive values can appear in logs, memory dumps, and error messages. Binary storage prevents the key value from appearing as readable text anywhere in the system. It wasn't in the spec — I identified it while thinking through how the key moves through the system end to end.

---

Q: The CLI returns the master key as plain text to the caller. Isn't that a security risk?

A: This is the disaster recovery flow — the admin is directly connected to the database via connection string in an air-gapped environment. The channel is already controlled and direct. The key is displayed to the admin and not stored by the CLI. The alternative would be encrypting the output, which requires the admin to have a decryption key — but in a disaster scenario where the admin is using this CLI, adding that dependency defeats the purpose. The design was intentional and accepted by the security reviewers.

---

Q: If the read-back fails, what does the service return to the caller?

A: It returns a 500 error indicating key persistence could not be confirmed. The caller knows the operation did not succeed and can retry. We don't return 204 unless the read-back confirms the key is actually in the database.

## 3A. Alternate Linux Bug

**STAR:**

Situation: I introduced a backend change in MobiControl that caused Linux devices to enter a continuous enroll-unenroll loop. The device would enroll, immediately unenroll, and keep repeating — Linux devices could not be managed through the platform at all.

Task: Identify the root cause precisely — not just find a workaround — and fix it without introducing new issues.

Action: I flagged it to the team immediately rather than quietly investigating — I didn't want others spending time debugging something I already suspected was mine. I reproduced the issue consistently and traced the full enrollment flow step by step through the state machine. The issue wasn't obvious because enrollment appeared to succeed on the surface before the unenroll triggered. I mapped exactly where in the state transition my change had broken the flow, understood why it broke it, and fixed it at the precise point of failure rather than working around it. I also added a regression test specifically covering this failure mode.

Result: Linux enrollment restored, verified against both cloud and on-prem configurations. Regression test now sits in the suite as a permanent guard.

---

**Deep follow-ups and answers:**

Q: How did you discover it — did someone report it or did you find it yourself?

A: I discovered it myself. After my change went in I was doing validation and noticed the enrollment loop behavior. I suspected it was related to my change immediately.

---

Q: How long did it take to identify the root cause?

A: It took me a few hours of tracing through the enrollment state machine to identify exactly where the transition broke. The challenge was that enrollment appeared to succeed initially — the break happened in a subsequent state transition, not the enrollment call itself.

---

Q: Did you tell your manager before or after you fixed it?

A: I flagged it to the team immediately when I identified it — before I had the fix. I didn't want to quietly investigate and then present a fix as if nothing had happened. Transparency first, then fix.

---

Q: What exactly was the test you added — what scenario does it cover?

A: The test covers the specific state transition that my change affected — verifying that after a successful enrollment the device stays in enrolled state rather than transitioning to unenrolled. It's a regression guard for this exact failure mode.

## 4. Buddy Help (Earn Trust), Linux Bug could be here(?)

**STAR:**

Situation: Two new college graduates joined our team recently and I was assigned as their buddy. They were given a technical debt reduction task as their first real contribution — migrating from INamedDependencyProvider to the native ASP.NET Core KeyedServices attribute across our codebase.

Task: Help them onboard and get to a point where they could contribute meaningfully on a real technical task quickly.

Action: Standard buddy responsibilities cover admin onboarding — processes, tools, introductions. But I could see they had no context for the technical task they'd been assigned. They didn't understand why INamedDependencyProvider was being replaced, what KeyedServices does differently, or how the change mapped to our existing codebase. Nobody asked me to help them with the technical side — I did it because I could see they would struggle without it. I walked them through the context of the migration, explained the difference between the two approaches, showed them the necessary code changes, and helped them raise their first PR — including how we structure PRs, what reviewers look for, and how to handle review feedback.

Result: They were able to contribute meaningfully on a real codebase task within their first week. Their first PR went through review successfully. They had the technical context to understand what they were doing and why, not just copy-paste changes blindly.

---

**Deep follow-ups and answers:**

Q: You said nobody asked you to help with the technical side. Why did you take that on when it wasn't your responsibility?

A: Because being a buddy only in the administrative sense wasn't actually useful to them. They had a real task with a real deadline and no context for it. If I just helped them with onboarding paperwork and left them to figure out INamedDependencyProvider vs KeyedServices on their own, I wouldn't have actually helped them. I took it on because I could see it was needed.

---

Q: What's the difference between INamedDependencyProvider and KeyedServices?

A: INamedDependencyProvider is a custom in-house abstraction for resolving named dependencies. KeyedServices is the native ASP.NET Core feature introduced in .NET 8 that does the same thing — resolving services by a key — but is built into the framework. The migration eliminates a custom abstraction in favour of the framework's native capability, which reduces maintenance overhead and aligns with the platform direction.

---

Q: What did you learn from helping them?

A: Explaining the difference between INamedDependencyProvider and KeyedServices to someone with no prior context forced me to understand the distinction more precisely than I had before. Teaching something always deepens your own understanding. I also learned that onboarding is more effective when you connect new joiners to real work early rather than keeping them in tutorial mode.

---

Q: How did you make sure you weren't just doing the work for them?

A: I walked them through the approach and showed them examples of the change pattern, but they made the actual code changes themselves. My role was to give them the context and confidence to do it, not to do it for them. The PR was theirs — I just helped them understand what good looked like before they submitted it.

--------------
## 5. Learn and Be Curious

Situation: When I transferred to the MobiControl team and was assigned the SOTI ONE Apps Visibility feature, I had no prior familiarity with the team's codebase or architecture. To implement the feature correctly I needed to understand how the Management Server and Deployment Server communicate — specifically how device check-ins flow through the system — because the entire feature depended on intercepting and processing data at the right point in that flow.

Task: Get deep enough on an unfamiliar distributed architecture in a short enough time to make correct design decisions before implementation began.

Action: I spent the first week purely on understanding before writing a single line of feature code. I read through the existing codebase, put debuggers at key points in the pipeline, and experimented with the system by triggering check-ins and observing what happened at each stage. The most important thing I discovered during this process was not in any documentation — web console interactions don't immediately trigger the agent. They live inside a .NET message queue and execute when the Deployment Server is ready to process them. Understanding that changed how I thought about the entire feature — it explained why the unchanged-snapshot problem exists and why the solution had to be at the database comparison level rather than the event level. By the time I started implementation I had a mental model of the full flow from agent check-in through snapshot processing through to the database that was accurate enough to make correct design decisions.

Result: That week of deliberate learning before implementation meant I didn't make design mistakes that would have been expensive to fix later. The unchanged-snapshot handling — which turned out to be one of the trickiest parts of the feature — I identified and designed a solution for before I started coding specifically because I understood the system deeply enough to anticipate the problem.

---

**Deep follow-ups and answers:**

Q: You said you discovered the message queue behavior wasn't in documentation. How did you figure it out?

A: By putting debuggers at different points in the pipeline and observing the actual execution flow. I triggered a web console interaction and traced what happened — the request didn't immediately reach the agent. It went into a queue first. Seeing that in the debugger made the architecture clear in a way that reading code alone hadn't.

---

Q: Why spend a full week learning before implementing — wasn't that wasting time given the one month deadline?

A: The opposite. A week of learning before implementation saved more than a week of rework after implementation. If I had started coding without understanding the message queue behavior and the unchanged-snapshot constraint, I would have built something that didn't account for those realities and had to redesign it mid-implementation. Front-loading the understanding protected the delivery.

---

Q: What would you have done differently if you had less time?

A: I would have been more targeted — identified the specific parts of the architecture that directly affected my feature and gone deep on those first, leaving the rest for later. The message queue behavior and the snapshot pipeline were the critical paths. Everything else could have waited.

---

Q: How do you approach learning an unfamiliar system quickly in general?

A: Read the code first to get the structure, then run it with debuggers to see the actual behavior, then experiment by triggering real flows and observing what happens. Documentation tells you what the system is supposed to do. Debuggers and experiments tell you what it actually does. The gap between those two is usually where the important things are.

## 6. Disagree and Commit

Situation: While implementing SOTI ONE Apps Visibility I needed to design the processing layer for app data extracted from device check-in snapshots. We have 7 SOTI ONE apps each with different data formats that needed to be ingested and stored.

Task: I proposed an initial design to the architecture team, they rejected it, and I needed to engage with their reasoning honestly and commit to whatever was decided.

Action: My initial proposal was to store the app data as raw JSON in the database — simple, generic, easy to implement, and requiring no per-app code changes when new apps are added. The architecture team rejected it with specific technical concerns: redundant headers being stored, inability to index properly on JSON fields, and stale references with no way to detect invalidation. I engaged with each concern individually rather than defending my proposal. When I worked through each problem I could see them clearly in my own design — they weren't vague objections, they were technically sound. My approach optimized for developer simplicity at the cost of database correctness at scale. I acknowledged that honestly, committed fully to the per-app processor pattern they proposed, and implemented all 7 processors, the shared extension table, and the bulk MERGE upsert without further pushback.

Result: The per-app processor architecture shipped and runs on 25 million devices. In retrospect the architecture team was right — JSON storage would have created real maintenance problems at our scale.

---

**Deep follow-ups and answers:**

Q: Did you push back at all when they rejected your proposal?

A: No. I engaged with each concern they raised and I could see the technical problems clearly in my own design. It wasn't deference — I independently validated that their reasoning was correct. There was no point in pushing back on something I could see was right.

---

Q: What specifically convinced you they were right?

A: The indexing problem was the clearest one. We're dealing with device check-ins at scale — 25 million devices. If the app data is stored as raw JSON you can't build efficient indexes on specific fields. Any query that needs to filter or sort by an app-specific field becomes a full table scan. That's not acceptable at our scale. Once I saw that clearly the other concerns — redundant headers, stale references — were also obviously real.

---

Q: Was there any part of their reasoning you still disagreed with after the discussion?

A: Not fundamentally. The one thing I still think about is that my approach would have made adding a new SOTI ONE app much simpler — just send a new JSON structure, no new code. With the per-app processor pattern, adding an 8th app means adding a new processor class. But that's a minor maintenance cost compared to the database problems my approach would have created. The tradeoff is clearly in the architecture team's favor.

---

Q: Once you committed, did you ever revisit the JSON idea?

A: No. Once the decision was made I committed fully. Revisiting it mid-implementation would have been disruptive and unproductive. The time to disagree is before the decision is made, not after.

---

Q: What would you do differently if you were designing this from the start today?

A: I would have consulted the architecture team earlier — before forming a strong opinion on the approach. I developed the JSON storage proposal independently and then brought it to review. If I had involved them in the design thinking earlier, we might have landed on the per-app processor pattern from the start and avoided the cycle of proposal, rejection, and redesign.

## 7. Are right a lot

Situation: During the design phase of SOTI's key storage service — built for EU compliance affecting enterprise customers managing over 25 million devices — the team was finalizing the authentication model for the disaster recovery CLI. The proposed scheme used username and password authentication.

Task: As the CLI owner I was reviewing the design and needed to validate whether the proposed authentication approach was actually correct for our specific deployment context.

Action: I thought through how username and password authentication works in practice for on-prem enterprise environments step by step. Each installation would need local user accounts. Those accounts would need to be created and managed locally. There would be no reliable way to trace which local account corresponded to which customer admin. In a break-glass scenario for master encryption key retrieval — the most sensitive operation in the system — not knowing who is actually accessing the system is a serious accountability gap. I didn't just flag a vague concern. I identified the specific structural problem and reasoned through an alternative independently: the installationID and registration code are already unique per customer installation, already exist in our system, and map directly to a specific customer account in the main MobiControl database. I raised this during the design review with the specific flaw and the alternative clearly articulated.

Result: The team agreed the username/password approach had the flaw I identified. The installationID and registration code model was adopted and is now in production. My assessment was validated by senior engineers on the team.

---

**Deep follow-ups and answers:**

Q: How confident were you when you raised it?

A: Confident enough to raise it clearly and specifically. I hadn't just had a vague feeling — I had worked through the specific problem of local user account management in on-prem environments and identified the exact accountability gap. When you can articulate a specific flaw with a specific alternative, confidence follows naturally.

---

Q: What was the initial reaction from the team when you raised it?

A: They engaged with it seriously. I presented the specific problem — local user accounts with no reliable admin traceability — and the alternative — installationID and registration code. The discussion was about whether the flaw was real and whether the alternative solved it. They concluded it did.

---

Q: What would you have done if they had rejected your alternative?

A: I would have asked them to explain specifically how the username/password scheme handles the accountability gap I identified. If they had a concrete answer I had missed, I would have updated my view. If they didn't, I would have documented the concern formally in the design doc so it was on record, and then implemented whatever was decided. Disagreement has a time — the design phase. After the decision is made you commit.

---

Q: How do you know your alternative was actually better and not just different?

A: The installationID and registration code solve the specific problem I identified — they are already unique per installation and directly tied to a specific customer account. Every access event is traceable to a specific customer without any local account management. The username/password scheme had no answer to that problem. That's not a matter of preference — it's a measurable difference in accountability.

---

Q: At 10 months of experience, what made you confident enough to challenge a design decision in a room with senior engineers?

A: The confidence came from having a specific technical argument, not from seniority. I wasn't saying "I disagree" — I was saying "here is the specific problem and here is a specific alternative." When you have that level of specificity the conversation becomes technical rather than hierarchical. Senior engineers respond to good technical arguments regardless of who makes them.



#### Oh that duplicate tab logout issue could be a good story for deep dive.


# Mapped Stories So far
- Ownership => SOTI One Apps
- Deep Dive => IDP User unable to logout
- Received critical feedback | Improved upon shortcomings => Compliance feedback story
- outside ur responsibility => Key Storage Services







# Tell me about a time you disagreed with your manager
soti one apps
identity provider bug -> deep dive, you had to dive into the system
device based filtering -> customer obsession
compliance review -> negative feedback
key storage service -> 
json storage proposal -> have backbone, disagree & commit


### 🔴 Tier 1 — Must be extremely strong

**1. SOTI ONE Apps**

- Deliver Results
- Ownership
- Bias for Action
- Customer Obsession
- Prioritization
- Tight deadline
- Cross-team collaboration
- Influence without authority
- Tradeoffs
- Descope
- Most challenging project
- Above and beyond

**2. Identity Provider bug**

- Dive Deep
- Learn and Be Curious
- Difficult problem
- Unfamiliar problem
- Independent work
- Challenging debugging
- Hypothesis → validation

**3. Key Storage**

- Ownership
- Have Backbone
- Disagree and Commit
- Simplification
- Influence
- Technical judgment
- Going beyond responsibility

---

### 🟠 Tier 2 — Very strong

**4. JSON storage**

- Failure
- Mistake
- Negative feedback
- Learning
- Weakness
- What would you do differently?

**5. Compliance review**

- Critical feedback
- Highest Standards
- Working with senior engineers
- Handling criticism
