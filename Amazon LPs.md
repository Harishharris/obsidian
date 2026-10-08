# Amazon does not like the word "we" always use "I"
# need to go through resume & projects

#### LP: Tell me about a time you took ownership of something beyond your assigned task.

> **Situation**
> At SOTI, MobiControl stored master keys — used to encrypt data encryption keys — directly within the application. There was no isolation, which meant a breach of the application layer would expose the keys entirely. 
> 
> **Task**
> I was tasked with designing and building a standalone Key Storage Service that would decouple master key storage from the main application, accessible via REST API for writes and CLI for disaster recovery. 
> 
> **Action**
> I took full ownership of the design document — I drove three MOM sessions with senior engineers and the DevOps team, made the call to enforce synchronous persistence (write then read-back before returning 204), and designed the CLI specifically for air-gapped disaster recovery so operators could still retrieve keys without network API access. I also decided to convert the Master Key from Base64 string to binary before DB storage to prevent string exposure in logs or memory dumps. 
> 
> **Result**
> The service isolated master keys from the application layer across both cloud and air-gapped deployments. It supported 7+ API endpoints with strong transactional guarantees, and the CLI gave operations teams a verified recovery path that didn't exist before.

**Cross-questions the BR will ask**

> Who asked you to identify the security gap — or did you find it yourself?
> 
> What would have happened if you hadn't raised it?
> 
> Was there pushback from anyone on the team about prioritizing this?
> 
> You mentioned disaster recovery — who owned that part and why?
> 
> How did you know the backup verification was critical before returning a success response?


#### LP: Tell me about a time you had to dig into technical details to make a key decision.

> Situation
> During the Key Storage Service design, we had two authentication options: proceed with Basic Auth using Registration Code and Installation ID, or wait for the Bearer token SDK that a separate team was building.  
> 
> Task
> I needed to make a concrete recommendation that balanced security, delivery timelines, and operational risk.  
> 
> Action
> I connected with Dymytriy Karpov's team directly to understand the SDK timeline and confirmed there was a bottleneck that could delay us. I documented both options formally in the design doc and presented the trade-off to the PM: if we waited for Bearer token, we risked a project delay with no firm date; if we used Basic Auth, we could ship with the existing security model that all other SOTI services already used. I recommended proceeding with Basic Auth with a documented migration path to Bearer token — and got alignment from Aleksandr Vlasov.  
> 
> Result
> We shipped on schedule using Basic Auth, with authentication headers consistent with the rest of the SOTI service ecosystem. The design doc captured the future migration path clearly so the next engineer could pick it up without re-investigating.

Cross-questions

> Why did you go with Basic Auth instead of Bearer token from the start?
> 
> What were the security trade-offs of that choice?
> 
> How did you validate that Registration Code + Installation ID was sufficient for your threat model?
> 
> Who made the final call — you or a senior engineer?
> 
> If you could go back, would you have pushed for Bearer token from the beginning?

#### LP: Tell me about a time you simplified something complex or built something innovative

> Situation
> I wanted a backend-as-a-service I could self-host on any machine without Docker, Postgres, or external service dependencies. Tools like Supabase and Firebase are powerful but they impose infrastructure requirements and aren't truly portable.  
>   
> Task
> I designed and built KeenBase — a backend platform that ships as a single Go binary with SQLite embedded, exposing REST APIs for data, auth, file storage, and rate limiting.  
> 
> Action
> The key design decisions were: use Go for its single-binary compilation model, use SQLite so the database is just a file, and build a runtime schema engine that reads collection definitions and generates DDL on the fly — no migrations, no ORM. I also built a pluggable file storage system where you can switch between local disk and S3 by configuration. The in-process job scheduler runs goroutines at configured intervals with lifecycle management so there's no external cron dependency.  
>
> Result 
> The entire platform runs from one binary. You drop it on a server, give it a config, and it's live. That's the simplification — what normally requires 3–4 infrastructure components is one process.

**Cross Questions:**

> Why Go — was there a specific reason you didn't use Node.js or Java?
> 
> What does "zero external dependencies" mean in practice — how did you achieve that?
> 
> Who uses KeenBase — did you build it to solve a real problem or was it just a learning project?
> 
> How does the runtime schema engine work — walk me through what happens when I define a new collection.
> 
> What was the hardest part to build and why?

#### LP: Tell me about a time you had to move fast without having all the information you wanted.

> Situation
> Clients managing large device fleets in MobiControl were spending significant time manually identifying the right devices because the filtering was too coarse — you couldn't combine multiple criteria or filter by device type in one step.  
> 
> Task
> I needed to improve the device selection workflow by introducing multi-level, multi-criteria filtering without breaking existing behavior for current clients.  
> 
> Action
> I shipped device-type–based filtering first as an isolated enhancement — it was the highest-impact, lowest-risk change. Once that was stable, I layered in the multi-criteria filtration logic. I validated the approach with quick testing cycles rather than waiting for a full design review, because the underlying data model was already well understood.  
>   
> Result
> Client operational effort in device selection dropped by roughly 60%, measured by comparing pre/post step counts for a standard fleet management workflow. It also reduced support tickets about device management.

**Cross-questions**

> How did you arrive at the 60% number — how did you measure that?
> 
> Was this your idea or did a PM/manager spec it out for you?
> 
> What risks did you accept by moving fast here?
> 
> What would you have done differently if you'd had more time?

### LP: Tell me about a time you had to deliver a significant piece of work under constraints.

> Situation
> As part of building the Key Storage Service and associated MobiControl backend work, I had to design and deliver production-ready APIs with full transactional guarantees — in a distributed system where air-gapped deployments were a real constraint.  
>   
> Task
> Deliver 7+ RESTful APIs that were secure, tested, and ready for both cloud and on-prem deployment — with Kafka integration where event-driven reliability was needed — while also coordinating with a DevOps team for pipeline setup.  
>   
> Action
> I applied TDD from the start using JUnit and Mockito, which meant I caught integration issues early rather than at the end. I structured the API layer following SOLID principles — separated controller, service, and data service layers — so each could be tested in isolation. For Kafka, I used it where we needed guaranteed delivery of events between services; for synchronous operations I ensured the service returned success only after verified persistence.  
>   
> Result
> All APIs shipped with integration test coverage, supporting both cloud and air-gapped deployments. The transactional design meant no partial writes or silent failures in production.

**Cross-questions**

> What were the constraints — time, team size, unclear requirements?
> 
> What specifically did you build vs what did others build?
> 
> Where did you use Kafka and why — why not a simpler approach?
> 
> What corners, if any, did you have to cut? How did you decide what was acceptable to cut?
> 
> How did you ensure quality while moving at pace — what did your testing approach look like?

### LP: Tell me about a time you disagreed with your team or manager and pushed back.

> Situation
> There was an expectation that the Key Storage Service would launch with Bearer token authentication, which was the more secure and future-proof approach. But the SDK providing that capability had a bottleneck with the team building it — no confirmed delivery date.  
> 
> Task
> I needed to give the PM a clear recommendation, even if it meant pushing back on an expectation.  
> 
> Action
> I directly connected with the SDK team lead to get a realistic timeline, confirmed there was no firm date, and then formally documented both options in the design doc — proceed with Basic Auth and ship on time, or wait and risk an open-ended delay. I presented this to the PM without softening it: the Bearer token approach was better long-term, but shipping on time with Basic Auth — consistent with every other service in the ecosystem — was the right call now. Once the PM agreed, I fully committed and made sure the migration path was documented so it wasn't forgotten.  
> 
> Result
> The project shipped on schedule. The decision was documented and traceable. I didn't just accept the ambiguity — I pushed for clarity and then committed to the outcome.

**Cross-questions**

> How did you raise the concern — in a meeting, async, one-on-one?
> 
> What was the other person's position and why did they hold it?
> 
> Once the decision was made, did you commit fully even if it wasn't your preferred outcome?
> 
> What would have happened to the project if you hadn't raised this?


Ownership -> Linux Enrollment
	