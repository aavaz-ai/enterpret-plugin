---
name: taxonomy-scope
description: How to count customer feedback by taxonomy scope with the Wisdom MCP's resolve_taxonomy_scope tool. Use only when the resolve_taxonomy_scope tool is available in this session; if it is not listed, ignore this skill.
---

# Skill: counting feedback by taxonomy scope (follow exactly)

You answer counting questions about customer feedback. The taxonomy scope for a subject is decided by the server, not by you, so that the same question gives the same number on every run.

## Procedure

1. Identify each distinct subject in the question (a product area, feature, complaint, request or praise). Most questions have one subject.
2. For each subject, call `resolve_taxonomy_scope` exactly once with:
   - `phrase`: the subject in the person's own words, kept complete. Keep feature names, tab names, product names and qualifiers exactly as written (for example "navigation in the subscribers page top-level tabs (Analytics, More)"). Do not shorten, paraphrase or translate it.
   - `scope_kind`: "product" when the wording names an area or feature ("about X", "the X page"), "opinion" when it names a complaint, request or praise ("complaining about X", "asked for X"), otherwise "unknown".
   - `question`: the full question text.
   - `window_start` and `window_end` whenever the question states or implies a date window: both or neither, inclusive, as YYYY-MM-DD.
3. `count` is the number of distinct feedback records of every category in the scope within the window: not users or accounts, and not only complaints, requests or praise. If the question asks for exactly that total, `count` is the answer for that subject. Report it with `count_cypher`. Do not write your own count query for the same subject and do not run `run_graph_query` to recount or double-check it.
   If the question counts users or accounts, keeps only complaints, requests or praise, groups the result or adds another filter, or if there is no `count` (no window was passed, or `warnings` say the scope is partial, the search was truncated or the count failed), count with `run_graph_query` using the exact `scope` record ids, the window and the `filter_hint`, plus those conditions.
4. If the tool returns an empty `scope`, say that no taxonomy node matches the subject and fall back to a content search; do not retry the tool with a reworded phrase. If it answers that the label search did not complete, call it once more with the same arguments.
5. If `count` is 0, report 0. A zero is an answer, not a failure.
6. Use `run_graph_query` only for parts of the question the tool does not cover (users or accounts, only complaints, requests or praise, breakdowns by source, sentiment or time buckets, other filters), and only with the exact `scope` record ids the tool returned.
7. Use `search_graph_values` for source names, metadata and other values that are not taxonomy topics. Do not use it to choose taxonomy nodes.

## Output

State the number and what it counts (feedback records, users or accounts), the scope the server chose (level and name), and the window. Keep the explanation short.
