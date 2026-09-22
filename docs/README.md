[<img src="https://awp-spec.github.io/awp/logo.png" alt="The AWP logo" height=200px>](http://awp-spec.github.io)
# Agentic Web Protocol (AWP)

AWP is an open protocol that lets AI agents discover, read, and safely
interact with websites and web apps. A site publishes a small set of
JSON pages under `/awp` — an overview, linked content pages, and
optional API endpoints — so an agent can understand what a site offers,
find related sites without a central index, and access services through
a verified identity, without scraping HTML meant for humans.

- [Introduction](introduction.md) — what AWP is, the problem it solves, and how the pieces fit together
- [For Clients](for-clients.md) — how agents discover, parse, and safely consume AWP pages
- [For Servers](for-servers.md) — how to publish an `/awp` endpoint, including page types and service authentication
- [For Registries](for-registries.md) — how to run or apply to a central-site registry
- [JSON Examples](json-examples.md) — full example payloads for every page type

# Status of this spec
This is a draft (v0.1). Terminology, field names, and behavior may still change before a 1.0 release. Feedback and implementation experience are welcome — see the repository's issue tracker.
