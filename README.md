# Repolex Knowledge Graph of sympy/sympy-live

RDF knowledge graph data for [sympy/sympy-live](https://github.com/sympy/sympy-live), parsed by [repolex](https://repolex.ai).

> **Note**: This data is experimental and subject to change without notice.

## How to use this data

The easiest way to get started is to install the [rlex](https://github.com/repolex-ai/rlex) query tool:

```bash
cargo install --git https://github.com/repolex-ai/rlex
```

Verify the install:

```bash
rlex --help
```

**rlex is designed to be used primarily by LLMs in a terminal.** Start up your favorite AI assistant and ask it to use rlex. It handles the SPARQL — you just ask questions in plain English.

To load this repo's data:

```bash
rlex download sympy/sympy-live
```

Consult `rlex --help` for other options, including SPARQL queries, HTTP server, and interactive visualization.

## Data structure

All data is stored as gzip-compressed [N-Quads](https://www.w3.org/TR/n-quads/) (`.nq.gz`), a standard RDF format that can be loaded into any triplestore or graph database.

```
.
├── aggregate
│   ├── ast
│   │   └── 2f4e47c221ce4d7c438528107336fabe66b5497b
│   │       └── chunk-001.nq.gz
│   └── repolex
│       └── 2f4e47c221ce4d7c438528107336fabe66b5497b
│           └── chunk-001.nq.gz
├── blob
│   ├── 01ac2a495a0e2fb6cfdea64d8f654b5d72f6eb3d.nq.gz
│   ├── 046173ef0dfda62900df3096d506bdf19d76a4c8.nq.gz
│   ├── 0d1143ea25e80337dc4107b6183be8be98ad64f2.nq.gz
│   ├── 18c5a4bf8173a9621ff678f865c2b41d07a6d8de.nq.gz
│   ├── 1ce8afb748e38b1ce10b61260933ddb8ffc0e92e.nq.gz
│   ├── 3547c0b2832d64e3d363e201968bf7f9b8a6ed73.nq.gz
│   ├── 405f6aa42b116b99531b6e60a46f90187ddd8d70.nq.gz
│   ├── 4f7e82d921a2a9aec19e2e7b03fb589bbd460887.nq.gz
│   ├── 513867559b9b8fc3862a1d261f4185104ff98007.nq.gz
│   ├── 5a829fc549c528e29c352c330d752a030d9b0b87.nq.gz
│   ├── 5a92f240dfd976413219589d3133736df0c7fde5.nq.gz
│   ├── 5e881278578188e7dfd5d632394eedc69074adf1.nq.gz
│   ├── 60b6f4a98792f986536e5ebf63e2a4a2eb0001b2.nq.gz
│   ├── 660ff6a2875bf944f2008a75b8114a534342ab39.nq.gz
│   ├── 67c948b0a27ead962c37c282c30d5cd882fa0f23.nq.gz
│   ├── 6a0fe01d0b56a44b3a1da51fa651836e190609e0.nq.gz
│   ├── 718b0eb51a4f9c62bca3fd7600e049aa6bead0ff.nq.gz
│   ├── 719dcc886c4519cd3bdd16544f83972162c8e7d8.nq.gz
│   ├── 78fd59c6e8ed392ab0b1d1a2380b1ba0001e31cc.nq.gz
│   ├── 7e5de17fb9c70fd9378bc43317032f6b816e8a5f.nq.gz
│   ├── 803baf5e2e33c668dd42ddc7583f34ca64076b11.nq.gz
│   ├── 950ecaeedf1b3684412252b1b55c660aa81f7e80.nq.gz
│   ├── a5f68c278ab91ea8c7daaeaed927e11c30e9b4d6.nq.gz
│   ├── b7c32d396ef111bdd2cfb400847c663301888fb2.nq.gz
│   ├── b803d35c5bcf152a491da774e1e95c588eacca8f.nq.gz
│   ├── b9d640f058c00d7358b8cfdab89bbcf5b0ff67fc.nq.gz
│   ├── bf6dd3d6830fc32bd68ce42dd09bacc5198fc133.nq.gz
│   ├── c7d5d429d664be885515f71d0956d4ef264c7097.nq.gz
│   ├── d35d38527f3a7ff1d7b0f438906fd93ddd60ddcc.nq.gz
│   ├── d70262e5ac99642d0edd1689a7261b4e8de0b8e4.nq.gz
│   ├── e69de29bb2d1d6434b8b29ae775ad8c2e48c5391.nq.gz
│   ├── eb8c65e5bd0e9b4dd7a1eeb4abc5d5a60ba66d8b.nq.gz
│   ├── eba5f052147e00e555a70d9c456fb8dbbbf839f8.nq.gz
│   ├── f8c8f68370fb947384d7671181b9b4f480d67c08.nq.gz
│   └── fb8a2eeacfdf6ef40252c9d1e1202c8ad9b56de8.nq.gz
├── branch
│   └── branch.nq.gz
├── commit
│   └── commit.nq.gz
├── filetree
│   └── 2f4e47c221ce4d7c438528107336fabe66b5497b.nq.gz
├── issue
│   └── issue.nq.gz
├── pr
│   └── pr.nq.gz
└── tag
    └── tag.nq.gz

13 directories, 43 files
```

| Directory | What it contains |
|-----------|-----------------|
| `blob/` | Per-file AST graphs, content-addressed by git blob SHA. Each file in the source repo gets its own graph. |
| `aggregate/ast/` | Combined AST graph per parsed commit. Merges all blob graphs for a snapshot of the entire codebase at that point. |
| `aggregate/lsp/` | Language Server Protocol enrichment: resolved symbols, definitions, references, and type information. |
| `aggregate/dataflow/` | Interprocedural data flow edges between functions and modules. |
| `aggregate/repolex/` | Combined graph (AST + LSP + dataflow) per commit. |
| `commit/` | Git commit metadata (author, date, message, parent links). |
| `branch/` | Branch metadata. |
| `tag/` | Tag metadata. |
| `filetree/` | File tree snapshots per commit (which files existed and their blob SHAs). |
| `audit/` | Code architecture and graph audit reports per commit. |

## Source repository

[sympy/sympy-live](https://github.com/sympy/sympy-live)

---
*Parsed on 2026-10-21 by [repolex](https://repolex.ai)*
