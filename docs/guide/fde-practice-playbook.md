# FDE practice playbook for AGH

[Project home](../../README.md) · [Documentation](../README.md) · [Why AGH](why-agh.md) · [Quickstart](quickstart.md)

This guide turns the work of a forward-deployed engineer (FDE) into a repeatable delivery loop for Agnes Harness (AGH). It is an original, AGH-specific field guide. It is not a translation or reproduction of the source book listed in [provenance](../maintainers/provenance.md).

## The delivery loop

An FDE works across customer context, software, and adoption. The job is complete when a real user can achieve an agreed outcome reliably, and the team can explain how the result was produced.

| Stage | Field question | AGH practice | Exit evidence |
| --- | --- | --- | --- |
| Discover | Which costly workflow should change first? | Interview the people doing the work; inspect the current process and systems; identify a narrow, measurable task. | A named user, current baseline, problem statement, and agreed success measure |
| Validate | Is the proposed workflow safe and useful? | Start with representative examples and read-only integrations. Record assumptions, data boundaries, failure cases, and human decisions. | A tested scenario set and explicit acceptance criteria |
| Integrate | What must connect at this customer site? | Implement a backend plugin or MCP connection; configure credentials and endpoints outside reusable code; validate permissions with the customer. | Integration checks, least-privilege access, and documented configuration |
| Deliver | Can the user complete the task in their workflow? | Compose tools, Skills, and role-specific panels. Keep consequential actions behind the supported approval path. | A working user journey with expected outputs and a reviewable task trace |
| Adopt | Does the change improve the real operation? | Observe use with customer consent, compare against the baseline, review failures, and refine the workflow. | Customer-accepted results and measured changes, with limits stated |
| Reuse | Which parts apply to the next deployment? | Package validated capabilities as plugins or Skills. Keep customer data, credentials, policy, and site-specific assumptions in deployment configuration. | Reusable components with version, owner, scope, and known limitations |
| Expand | What is the next valuable slice? | Prioritize the next workflow from observed user needs and evidence, then repeat discovery. | A jointly agreed follow-up backed by observed demand |

## Start with a bounded problem

Avoid beginning with “add an agent.” Describe the current work in operational terms:

- **User and decision:** who performs the work, and what decision or action is needed?
- **Trigger and inputs:** what starts the task, and which records or systems provide the facts?
- **Current path:** how is it done today, including handoffs and exceptions?
- **Cost of failure:** what happens when the result is late, wrong, incomplete, or unauthorized?
- **Success measure:** which observable result would justify adoption?
- **Boundary:** which actions remain human decisions, and which data or systems are out of scope?

Use a small set of real, permissioned examples. Include routine cases, edge cases, and cases where the correct result is to stop or ask a person. A demo that works only on a hand-picked happy path is not deployment evidence.

## Design the integration around the customer's environment

For each connected system, document the owner, purpose, identity, permissions, data returned, write capability, timeout behavior, and failure response. Prefer the narrowest capability that can support the agreed workflow.

In AGH:

1. Use a **backend plugin** for a capability the deployment owns and needs to version.
2. Use **MCP** when connecting to an existing compatible service.
3. Use a **Skill** for reusable task instructions, checks, and decision procedures.
4. Use a **frontend panel** when the role needs a purpose-built view or controlled interaction.
5. Keep endpoints, credentials, and site policy in deployment configuration. Do not put secrets in Skills, example files, or logs.

Read [security and trust](security.md) before enabling a package or exposing a tool. Ordinary backend plugins run as trusted in-process code; package integrity records and approvals do not sandbox arbitrary plugin code.

## Make every important result checkable

For each task, define what a reviewer needs to see:

- the request and relevant scope;
- the records or sources consulted;
- the model and tools used;
- the approvals required and received;
- the output, including uncertainty and unresolved cases;
- a verification step tied to the source system or an independent check.

A trace helps explain execution; it does not by itself prove that a business outcome is correct. Validate consequential values against authoritative systems and ask a qualified person to review decisions that require judgment.

For changes to customer data, define authorization, idempotency, rollback or compensation, and post-action verification before enabling writes. Start in read-only mode where possible.

## Measure value without overstating it

Choose one primary outcome with the customer, then track the conditions that explain it. Examples include time to complete a case, queue age, rework rate, exception escape rate, or percentage of eligible cases handled without escalation.

Record:

- the baseline period and its data source;
- the post-deployment period and comparable workload;
- the denominator and exclusions;
- human review and escalation rates;
- errors, reversals, and incidents;
- any operational changes that could explain the difference.

Report observed results with their scope and limitations. Do not convert a small pilot, a synthetic benchmark, or model output quality into a claim of customer savings without supporting evidence.

## Turn delivery into reuse

Before calling a component reusable, write down:

- which behavior is common and which remains customer-specific;
- required permissions, configuration, and dependencies;
- supported inputs, outputs, and failure modes;
- owner, version, test coverage, and upgrade path;
- data retention and privacy expectations;
- a representative acceptance test that can be rerun.

A reusable plugin or Skill is a starting point for another deployment, not proof that the next customer's workflow or policy is identical. Revalidate it in the new environment.

## A practical first engagement

1. Agree with one customer user on a single workflow and success measure.
2. Map the data sources, permissions, human approvals, and failure cases.
3. Build a read-only end-to-end example with representative cases.
4. Review its outputs and trace with the people who own the process.
5. Add write actions only after authorization and recovery behavior are agreed.
6. Run a bounded pilot and compare results with the recorded baseline.
7. Capture the validated method and integration boundary in a Skill or plugin.
8. Share the results, limitations, and next decision with the customer.

Continue with [Why AGH](why-agh.md), [backend plugins](../develop/backend.md), [Skills](skills.md), [MCP](mcp.md), and [security and trust](security.md).

## Source note

The chapter map and themes are informed by 范冰 (Fan Bing, XDash), *前线部署工程师：人工智能时代的客户价值交付秘籍* (*Forward-Deployed Engineer: A Guide to Customer Value Delivery in the AI Era*), especially its treatment of problem selection, customer engagement, deployment, retention, expansion, repeatability, cases, ethics, metrics, and references. This page summarizes those themes in original language and applies them to AGH; it does not reproduce or translate the book's chapters. See the source repository and its sharing terms in [provenance](../maintainers/provenance.md).
