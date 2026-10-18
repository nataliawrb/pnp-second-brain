# Why GitHub, Not Google Drive

- **Diff and history are the review mechanism** — a pull request *is* the governance workflow; Drive has comments and version history, not an approval gate.
- **Markdown is what an AI context window wants** — a flat, well-structured `.md` file is far more reliably parsed than a Drive doc's formatting or a loose folder hierarchy.
- **Grep-ability and structure** — this flat topic layer is natively walkable by both humans and agents. Drive search is full-text and flat.
- **Portability** — "plug and play into other teams' local Claude environments" means pointing a context reference at a URL or a cloned path. A Drive folder needs per-environment connector setup; a GitHub repo doesn't.
- **Honest trade-off**: GitHub has a steeper floor for a non-technical contributor who's never used Git. Solve it with a thin contribution layer (a form, or a Claude-guided prompt that commits the Markdown on their behalf) rather than pretending the friction doesn't exist.
