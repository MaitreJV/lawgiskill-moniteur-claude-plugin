# LawgiSkill Moniteur

LawgiSkill Moniteur lets Claude run a limited, read-only keyword search of Belgian Official Gazette (Moniteur belge / Belgisch Staatsblad) publication metadata, in French or Dutch, with optional publication-date filters. Results can include the title, NUMAC, publication and promulgation dates, and a link to eJustice, the official publication source. A citation skill tells Claude how to present these results and their coverage limits.

The service is free and needs no account, API key or token.

Published by Online Solution Attorney SRL (OSA), Brussels — <https://lawgi.tech>.

## What the plugin contains

| Component | Purpose |
| --- | --- |
| `.mcp.json` | References the remote MCP server `https://moniteur-mcp.lawgi.tech/mcp` (no authentication). It exposes one read-only tool, `moniteur_rechercher`. |
| `skills/moniteur-citations/` | Instructions for searching and for citing results: dated references, eJustice links, reported limits, honest handling of empty results and errors. |
| `assets/lawgiskill-logo.png` | Listing icon. |

The plugin contains no executable code, hooks, commands or agents.

## The search tool

`moniteur_rechercher` accepts:

- `query` (required): plain keywords, 3 to 500 characters, no boolean operators or wildcards;
- `langue`: `fr` (default) or `nl`;
- `date_publication_debut`, `date_publication_fin`: publication-date filters, `YYYY-MM-DD`;
- `limite`: 1 to 10 results (default 5); `offset`: 0 to 100.

There is no NUMAC-only lookup and no date-only listing. Each response reports coverage indicators from the search engine (mode, retained and ignored terms, partial results, interrupted fallback).

## Sources and limits

- Searches run on publication metadata indexed through ETAAMB, the index used by the LawgiSkill service. Links point to eJustice, the official publication source. Only the official publication is authoritative.
- Completeness and freshness of the index are not guaranteed. **An empty result does not prove that a publication does not exist.** A service error is reported as an error, never as an empty result.
- The service returns publication metadata only: no consolidated texts, no in-force status, and no legal advice.
- Usage is subject to shared rate limits and a daily quota; when they are reached the tool returns an error and you can retry later.

## Example prompts

- "Search the Moniteur belge for publications about cybersecurity."
- "Zoek publicaties in het Belgisch Staatsblad over gegevensbescherming."
- "Find publications about 'intelligence artificielle' published in January 2024."

## Data and privacy

When Claude calls the tool, the search parameters (keywords, language, dates, pagination) are sent over HTTPS to `moniteur-mcp.lawgi.tech`, operated by OSA. The relay forwards them to the LawgiSkill search service using a service credential held on the server; users never provide or see a credential. The plugin sends nothing else and reads no local files or environment variables.

Do not put personal data in search keywords. Processing by OSA, including technical logs and retention, is described in the privacy policy: <https://lawgi.tech/legal/privacy/>. Contact: <https://lawgi.tech/contact/>.

## Support

- Website: <https://lawgi.tech>
- Support: <https://lawgi.tech/contact/>
- Terms: <https://lawgi.tech/legal/cgu/>

## License

MIT — see [LICENSE](LICENSE). The license covers the files in this repository (manifest, skill text, documentation). It does not grant rights to the LawgiSkill name and logo, or to the remote service.
