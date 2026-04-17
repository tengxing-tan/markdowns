# Sprint Planning

- [ ] Capacity
- [ ] setup sprint board: move incomplete item, calc effort point
- [ ] Forecast Velocity
- [ ] Tidy up sprint board, set remaining effort of the PBIs in new sprint board
- [ ] Pick up PBIs
- [ ] Sprint goal
- [ ] set demo item
- [ ] regression test
- [ ] Summary in email, send to product owner
- [ ] List work item to be refined with team/product owner, send email

# Scrum or waterfall

[Sprint vs mini-waterfall](https://www.linkedin.com/posts/vibhorchandel_why-sprints-are-blamed-for-being-mini-waterfalls-activity-7267560640423051267-aiL7?utm_source=share&utm_medium=member_desktop) - Sprint act like mini waterfall because: 1. Contractual stakeholder (people who follow fixed scope); 2. New joiner

# Refinement

Sprint refinement is a meeting to discuss the To do work items, ensure clear description, acceptance criteria, risk, and come up with any concerns.

# PBI Breakdown Guidelines

## Core Principle

When breaking down large PBIs into smaller ones:

- **Each small PBI should contain no more than 2 validation/business logic rules**
- DB changes can be mixed with frontend & backend work, or kept in separate PRs as needed
- Focus on logical unit completion, not technical layer separation

## Complexity Estimation (Story Points/Effort)

- Smaller PBIs are easier to estimate and have lower risk of scope creep
- Each PBI with 1-2 logic rules typically corresponds to 2-5 story points (depending on implementation complexity)
- Validate estimated effort against historical velocity to ensure realistic sprint planning

## Acceptance Criteria Examples

Each small PBI should define clear acceptance criteria that map to its validation rules:

- "When [condition], then [specific behavior]"
- "The system validates [specific rule 1]"
- "The system validates [specific rule 2]"
- Include both happy path and edge case validation criteria

## Testing Strategy

- Each validation/business logic rule should have corresponding unit test coverage
- With max 2 rules per PBI, testing scope remains focused and maintainable
- Consider test pyramid: unit tests (most), integration tests (middle), E2E tests (least)
- Testing effort should not inflate story points—it's part of "done" definition

## PR Review Strategy

- Small, well-scoped PBIs lead to focused, reviewable PRs
- Allow DB changes and feature implementation in same PR if they're tightly coupled
- Use separate PRs when DB change can be deployed independently or has schema impact
- Link related PRs with clear commit messages noting dependencies
