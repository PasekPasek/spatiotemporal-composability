# Spatiotemporal Composability, Explained Interactively

A single-page, dependency-free interactive explainer for **revertible effects** and **reactive coeffects** — the two mechanisms behind [*A Programming Paradigm for Spatiotemporal Composability*](https://arxiv.org/abs/2608.25512) (Shi, Zhang & Cui, arXiv:2608.25512, cs.PL).

**Live: https://pasekpasek.github.io/spatiotemporal-composability/**

## What's in it

- **A runtime sandbox.** Four components with declared `inject` and `provide`. Install and remove them in any order and watch the service table Σ and the inverse stack φ react. Removing `database` cascades through `auth` and `commands`, deepest dependent first.
- **track / recover.** Step through effects being applied and unwound, one inverse at a time, in the correct reverse order.
- **The fiber lifecycle.** All nine rules of the calculus over Inactive → Reloading → Active → Unloading (plus the empty node), including `L-Divert` — what happens when a dependency changes halfway through activation — and the retire/remove split that stops an Active fiber from being dropped with its accumulator still full.
- **Confluence.** Two different operation histories, same final configuration, with the theorem's actual hypotheses spelled out.
- **TypeScript throughout**, including a ~30-line `Ctx` class that contains the entire temporal mechanism.

## Running it

It's one file with no build step.

```bash
python3 -m http.server 8000   # then open http://localhost:8000
```

## Accuracy

The page was checked line by line against the paper (arXiv PDF, 85 pp.). Where an earlier draft
diverged, the paper wins: the lifecycle state is `Reloading` not `Loading`; `O-Insert` registers a
fiber as `Inactive` rather than starting its activation; the `Active → Unloading` edge is `L-Leave`,
not `O-Remove`; removal is split across `O-Retire` / `L-Leave` / `L-Unload` / `O-Remove`; the Cordis
v4 instantiation API is `ctx.use`, not `ctx.plugin`; and confluence is stated with its real
hypotheses (quiescence, totality on provision, orchestration held fixed).

## Deploying

**Settings → Pages → Source: Deploy from a branch → `main` / `root`**. For a custom domain, add a `CNAME` file containing the bare domain and point a DNS `CNAME` record at `PasekPasek.github.io`.

## Credits

The paper is by Yifan Shi, Wei Zhang and Tianyi Cui; the reference implementation is [Cordis](https://github.com/cordiverse). This page is a teaching simplification — the formal content (effect iterators, observational equivalence, the metatheory of the calculus) is in the paper.

Built by [Paweł Pasek](https://github.com/PasekPasek).
