
1. Model the CourseEnrollment Aggregate Root
In Domain‑Driven Design (DDD), the aggregate root is the central object that controls consistency and rules for related entities.

Here, CourseEnrollment is the aggregate root because it manages the relationship between a course and its enrolled students.

All actions (enroll, drop, check capacity) must go through this root to ensure rules are respected.

Think of it as the “gatekeeper” — no student can be added or removed without CourseEnrollment’s approval.



2. Enforce Invariant Limits
Invariants are rules that must always hold true in the system.

For CourseEnrollment, examples include:

Capacity limit: A course cannot exceed its maximum number of students.

No duplicates: A student cannot enroll twice in the same course.

Consistency: Dropping a student should only be possible if they are already enrolled.

These invariants prevent invalid states (like over‑enrollment or ghost students) and keep the system trustworthy.

3. Emit Domain Events
Domain events capture important business happenings that other parts of the system may care about.

Examples in CourseEnrollment:

StudentEnrolledEvent: Triggered when a student successfully joins a course.

StudentDroppedEvent: Triggered when a student leaves or is removed.

These events allow other systems (like notifications, billing, or transcripts) to react without tightly coupling them to the enrollment logic.

It makes the system more extensible and responsive to real‑world needs.

DDD Diagram
CourseEnrollment (Aggregate Root)
   ├── Course (Entity)
   ├── Student (Entity)
   └── EnrollmentRecord (Value Object)

Rules (Invariants):
   - Max capacity enforced
   - No duplicate enrollment
   - Drop only if enrolled

Events:
   - StudentEnrolledEvent
   - StudentDroppedEvent
   - CourseCapacityReachedEvent
