# Prototyping a design

A prototype answers a design question and is then discarded. Its output is a verdict, not a foundation.

- The prototype MUST be chartered by the questions it must answer (e.g., what is infeasible, what can be reused, how much effort this is, what capacity it needs), never by a demonstration. Those questions MUST be written down before the design is.
- Effort MUST go to the parts whose feasibility is in doubt, which are the ones we have least experience of. Parts already known to work MUST be stubbed or left out, and the omission MUST be stated.
- Where the prototype's behaviour differs from what production would require, the difference MUST be marked at the place where it's cut, so that it can't be mistaken for a decision.
- The design MUST be published before the code exists, and the document MUST be the artefact put to reviewers, including reviewers outside the team.
- A document that is not yet a specification MUST say so, and MUST state what would make it one.
- Every design document MUST carry a maturity marker and a changelog, and MUST be demoted where it turns out to be unfinished.
- The prototype MUST end with a written verdict, and every finding that changes the design MUST become tracked work.
- A prototype MUST be archived and labelled as throwaway once its questions are answered, naming its successor.
