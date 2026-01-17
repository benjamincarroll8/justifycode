# JustifyCode Setup Guide

This guide explains how to set up JustifyCode with JustifyMCP integration for JustifyLocal developers.

## Prerequisites

- Node.js 18+ or Bun
- Python 3.11+ (for JustifyMCP)
- Access to the private JustifyMCP repository

## Quick Start

### 1. Install JustifyCode

```bash
npm i -g justifycode
```

### 2. Clone and Set Up JustifyMCP (Private Repo)

```bash
cd ~/Desktop/JustifyLocal
git clone https://github.com/YOUR_ORG/JUSTIFYMCP.git
cd JUSTIFYMCP

python -m venv venv
.\venv\Scripts\activate  # Windows
pip install -e ".[dev,local]"

cp env.example .env
# Edit .env with your Cloud SQL credentials
```

### 3. Configure API Keys

```bash
python scripts/setup_user.py
```

### 4. Enable JustifyMCP

Create `~/.opencode/opencode.json`:

```json
{
  "mcp": {
    "justifymcp": {
      "enabled": true
    }
  },
  "tools": {
    "justifymcp_*": true
  }
}
```

### 5. Start JustifyMCP Server

```bash
python -m justifymcp.server
```

### 6. Start JustifyCode

```bash
justifycode
```

## Available Tools (28 Total)

- **Client Context**: get_client, search_client_docs, list_clients, add_client_context, ingest_document
- **Competitor**: add_competitor, get_competitor_snapshot, compare_client_vs_competitors, get_competitor_gaps
- **Research**: deep_research, research_for_client, get_local_seo_trends, analyze_serp
- **GBP**: get_gbp_profile, update_service_areas, list_gbp_reviews, create_gbp_post
- **Rankings**: get_rankings, compare_rankings_over_time, audit_citations, get_citation_status
- **Dev Context**: get_tech_stack, list_internal_tools, get_tool_code, add_tool_to_registry
- **Datasets**: generate_client_dataset, generate_niche_dataset, export_for_training

## Security

- JustifyMCP runs on localhost:8000 only
- Disabled by default in JustifyCode
- No credentials in public repo

