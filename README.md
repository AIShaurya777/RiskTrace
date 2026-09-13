# RiskTrace

RiskTrace is a supply chain risk analysis tool for open-source software dependencies. It scans a GitHub repository, extracts direct and transitive dependencies, matches them against known vulnerability databases, and produces a risk score with actionable recommendations.

## Team

| Name | Roll Number |
|------|-------------|
| Shaurya Sangwan | 1024030462 |
| Abhishek Batra | 1024030463 |
| Sushain Sharma | 1024030439 |

## Directory Structure

```
RiskTrace/
├── .github/
│   └── workflows/
│       └── deploy-pages.yml        # GitHub Pages deployment workflow
├── code/
│   ├── backend/                    # Node.js + Prisma + PostgreSQL API
│   ├── frontend/                   # React + Vite + Tailwind UI
│   ├── docker-compose.yml          # Multi-container Docker setup
│   ├── .env.example
│   └── README.md                   # Code-specific setup instructions
├── docs/
│   ├── diagrams/                   # UML & architecture diagrams (activity, architecture, data-flow, ER, use-case)
│   ├── gantt-chart-risktrace.xlsx  # Project Gantt chart
│   └── idea-pitch-ppt.pdf         # Project pitch presentation
├── github-pages/                   # GitHub Pages project website (HTML/CSS/JS)
├── journals/                       # Individual contribution logs per team member
├── proposal/                       # Project proposal (LaTeX + PDF)
├── prototype/                      # Prototype report
└── README.md
```

## Datasets

- [OSS Vulnerabilities Dataset (Kaggle)](https://www.kaggle.com/datasets/japkeeratsingh/oss-vulnerabilities/data)
- [Malicious Software Packages Dataset (DataDog)](https://github.com/DataDog/malicious-software-packages-dataset)

## Code

For the full source code and setup instructions, refer to the [`code/`](./code/) directory. It contains the backend (Node.js + Prisma + PostgreSQL) and frontend (React + Vite) applications along with Docker configuration.
