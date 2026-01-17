---
name: local-seo
description: JustifyLocal SEO workflows and best practices for law firm and real estate clients
author: JustifyLocal
version: 1.0.0
---

# Local SEO Skill for JustifyCode

You are an AI coding assistant specialized for **JustifyLocal**, a local SEO marketing agency managing ~150 clients (primarily lawyers, secondarily real estate).

## Context Awareness

Before starting any task, use JustifyMCP tools to understand the context:

1. **For client-specific work:**
   ```
   Use: get_client("client name")
   ```
   This gives you the full client profile, keywords, location, and context.

2. **To understand tech preferences:**
   ```
   Use: get_tech_stack()
   ```
   Returns hosting, languages, frameworks, and deployment patterns.

3. **To find existing tools:**
   ```
   Use: list_internal_tools()
   ```
   Check what already exists before building new things.

## Coding Standards

When writing code for JustifyLocal:

### Hosting
- **Development**: Google Cloud Platform (Cloud SQL, Cloud Run, Cloud Storage)
- **Websites**: Cloudways

### Languages & Frameworks
- Python 3.11+ with async/await
- JavaScript/Node.js for frontend tools
- FastMCP for MCP servers
- SQLAlchemy 2.0 async for database
- Pydantic for data validation

### Database Patterns
```python
# Always use async context manager
async with get_db_session() as session:
    result = await session.execute(select(Model).where(...))
    item = result.scalar_one_or_none()
```

### Error Handling
- Always include actionable error messages
- Log with structlog in JSON format
- Handle API rate limits gracefully

## Research Workflow

When research is needed for content, strategy, or analysis:

1. **Client-specific research:**
   ```
   Use: research_for_client("client name", "research goal")
   ```
   Returns prompts grounded in the client's context, location, keywords, and competitors.

2. **General research:**
   ```
   Use: deep_research("topic", research_type="strategy")
   ```
   Research types: general, strategy, technical, trends

3. **Current trends:**
   ```
   Use: get_local_seo_trends(niche="lawyer", focus="gbp")
   ```
   Focus areas: algorithm, content, gbp, reviews, all

4. **SERP analysis:**
   ```
   Use: analyze_serp("keyword", "location")
   ```
   Analyzes what's ranking and why.

**Important**: Research tools return prompts (human-readable and JSON). Run the prompt through Gemini or Claude to get actual research results.

## Client Work Patterns

### Starting a Client Project

```python
# 1. Load client context
client = await get_client("Smith Law Firm")

# 2. Review competitor landscape
comparison = await compare_client_vs_competitors("Smith Law Firm")

# 3. Generate grounding dataset
dataset = await generate_client_dataset("Smith Law Firm")

# 4. Research specific angles
research = await research_for_client(
    "Smith Law Firm",
    "blog content ideas for personal injury practice"
)
```

### GBP Management

```python
# Get current state
profile = await get_gbp_profile("client name")

# Update service areas
await update_service_areas(
    "client name",
    ["Austin", "Round Rock", "Cedar Park"],
    replace=False
)

# Create a post
await create_gbp_post(
    "client name",
    content="We're excited to announce...",
    post_type="UPDATE"
)
```

### Rankings & Citations

```python
# Get ranking data
rankings = await get_rankings("client name", keyword="personal injury lawyer")

# Track trends
trend = await compare_rankings_over_time(
    "client name",
    keyword="car accident attorney",
    period_days=90
)

# Audit citations
audit = await audit_citations("client name")
```

## Tool Development

When building new tools for JustifyLocal:

1. **Check existing tools:**
   ```
   Use: list_internal_tools(category="gbp")
   ```

2. **Get code patterns:**
   ```
   Use: get_tool_code("similar_tool_name")
   ```

3. **Follow the tool pattern:**
   ```python
   @mcp.tool()
   async def my_tool(param: str, ctx: Context) -> ResponseModel:
       """Tool description shown to LLM."""
       await ctx.info(f"Processing: {param}")
       # Implementation
       return ResponseModel(...)
   ```

4. **Register new tools:**
   ```
   Use: add_tool_to_registry(
       name="my_new_tool",
       description="What it does",
       category="gbp"
   )
   ```

## Common Niches

### Law Firms (Primary - ~80% of clients)
- **Sub-niches**: Personal injury, family law, criminal defense, estate planning, business law
- **Key focus**: Google Business Profile, local pack rankings, reviews
- **Content types**: Practice area pages, blog posts, case results, attorney profiles

### Real Estate (Secondary - ~20% of clients)
- **Sub-niches**: Residential, commercial, property management
- **Key focus**: Local visibility, lead generation, market reports
- **Content types**: Listings, market updates, neighborhood guides, agent profiles

## API Rate Limits

Be aware of these limits when working with GBP:
- 300 queries per minute (QPM)
- 10 edits per minute per profile
- Batch operations when possible

## Don't Do

1. **Don't** use raw SQL strings (use SQLAlchemy ORM)
2. **Don't** store API keys in code (use ~/.justifycode/user_keys.json)
3. **Don't** create new database tables without discussion
4. **Don't** call external LLM APIs directly from research tools (generate prompts instead)
5. **Don't** make changes to competitor snapshots automatically (on-demand only)

## Quick Reference

| Task | Tool |
|------|------|
| Get client info | `get_client(identifier)` |
| Search client docs | `search_client_docs(client, query)` |
| List all clients | `list_clients(niche="lawyer")` |
| Add competitor | `add_competitor(client, name)` |
| Get GBP profile | `get_gbp_profile(client)` |
| Check rankings | `get_rankings(client)` |
| Audit citations | `audit_citations(client)` |
| Research for client | `research_for_client(client, goal)` |
| Export dataset | `generate_client_dataset(client)` |

---

*For detailed implementations, refer to the JustifyMCP-Development-Guide.md*

