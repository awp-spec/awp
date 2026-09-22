# Introduction

## What AWP is

The Agentic Web Protocol (AWP) is an open protocol that lets AI agents
discover, read, and interact with websites and web apps through a
dedicated machine-readable interface, separate from the human-facing
HTML.

A site that supports AWP serves a small set of JSON pages under
`/awp`. These pages describe what the site offers, link to more
detail, and — optionally — expose existing APIs to authenticated
agents. An agent that finds a site's `/awp` endpoint can understand
what the site does, navigate its content, discover related sites, and
call its services, all without parsing HTML written for humans.

AWP is, in part, an amalgamation of ideas that already exist
separately on the web today:

| AWP provides...            | ...roughly like     |
|-----------------------------|----------------------|
| A sitemap of AWP pages      | `sitemap.xml`        |
| Plain-language descriptions | `llms.txt`           |
| Authenticated API access    | REST/OpenAPI, MCP    |
| A way to find related sites | search engines       |

What's new is combining these into one endpoint, and adding two
things the web doesn't have yet: a way for agents to find related
sites **without a central index**, and a way for a site to know
**which agent tool** is calling, with a cryptographic guarantee.

## The problem

Agents today mostly interact with the web the way a browser does:
they load HTML built for human eyes, and try to infer structure and
meaning from it. This works, but it's fragile, wasteful, and gives
sites no way to say "here's what I actually offer" directly to an
agent, or to distinguish agent traffic from a human clicking around.

Existing pieces solve parts of this. `llms.txt` gives agents a plain
text description. MCP gives agents structured tool access. Neither
solves discovery at web scale: how does an agent find *other* sites
relevant to what it's doing, without a search engine or a central
directory controlled by one company?

## The AWP approach

AWP addresses this with a few core ideas:

- **One endpoint, `/awp`, serves everything.** A site publishes JSON
  pages describing itself, its content, and (optionally) its
  services — no separate systems to maintain.
- **Pages link to each other, both for humans and machines.**
  Content pages use ordinary Markdown links plus a matching
  machine-readable list, so both an LLM reading prose and a strict
  validator can navigate the same site.
- **Discovery is distributed, not centralized.** Each site can list
  related sites, and can point at one or more central sites per
  category — like Mouser for electronic component distributors — to
  bootstrap discovery within an industry, without depending on any
  single index of the whole web.
- **Central-site lists are opt-in and pluralized.** A site chooses
  which registries (if any) to trust for suggested central sites.
  Anyone can run a registry; none is required, and none is
  authoritative.
- **Agent identity is signed, not just asserted.** When a site wants
  to know which agent tool is calling — for example, to grant access
  to a service endpoint — the agent presents a JWT signed by the
  tool's own key, verifiable without a shared registry or database.
- **AWP content is untrusted input, never instructions.** Any text an
  agent reads from an AWP page — descriptions, Markdown content,
  summaries — is data to reason about, not commands to follow. This
  matters more for AWP than most protocols, since AWP content is
  built specifically to be read by language models.

## Who this documentation is for

This spec is split by role, so you can read only what applies to you:

- **[For Clients](for-clients.md)** — building an agent or agent tool
  that consumes AWP pages: discovery, parsing, and safety rules.
- **[For Servers](for-servers.md)** — publishing an `/awp` endpoint on
  your site: page types, required fields, and service authentication.
- **[For Registries](for-registries.md)** — running or applying to a
  central-site registry.
- **[JSON Examples](json-examples.md)** — full example payloads for
  every page type, for quick reference.

## Status of this spec

This is a draft (v0.1). Terminology, field names, and behavior may
still change before a 1.0 release. Feedback and implementation
experience are welcome — see the repository's issue tracker.
