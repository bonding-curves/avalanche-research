# Avalanche Economic Data Snapshots

This directory contains timestamped data snapshots that serve as the single source of truth for Avalanche network metrics used throughout the economic modeling project.

## Purpose

The snapshot system addresses the problem of **data inconsistency** across multiple documents by:
1. Centralizing all network metrics in timestamped files
2. Providing clear source citations for each data point
3. Documenting data quality and known gaps
4. Enabling temporal analysis of network evolution

## Structure

```
content/data/
├── README.md                    # This file
├── snapshot-YYYY-MM-DD.md       # Individual timestamped snapshots
└── snapshot-latest.md           # Symlink to most recent snapshot (optional)
```

## Using Snapshots

### For Reading Data

When you need Avalanche network metrics for your work:

1. **Find the most recent snapshot** matching your analysis period
2. **Check the data freshness table** to understand recency of each metric
3. **Review the data quality assessment** to understand confidence levels
4. **Cite the snapshot** in your document using this format:

```markdown
Staking ratio: 57.8% [Source: snapshot-2025-11-28.md]
```

### For Creating Documents

When creating new analysis documents, economic models, or research:

1. **Always reference a specific snapshot** rather than copying data
2. **Link to the snapshot file** so readers can access full context
3. **Note which metrics are critical** to your analysis
4. **Document assumptions** made when data has gaps

### Example References

```markdown
According to the [November 2025 snapshot](../data/snapshot-2025-11-28.md),
the network has 1,539+ validators staking 248M AVAX (57.8% of circulating supply).
```

## Creating New Snapshots

### When to Create

Create a new snapshot when:
- **Weekly routine:** Every 7 days for regular tracking
- **Major events:** Network upgrades, significant metric changes
- **Before modeling:** Start of new economic analysis work
- **Data updates:** When critical metrics have materially changed

### How to Create

#### 1. Prepare Data Collection

Gather data from these primary sources:

**Market Data:**
- [CoinMarketCap - AVAX](https://coinmarketcap.com/currencies/avalanche/)
- [CoinGecko - AVAX](https://www.coingecko.com/en/coins/avalanche)

**Network Metrics:**
- [Avascan Statistics](https://avascan.info/stats/staking)
- [Avalanche Stats Dashboard](https://stats.avax.network/dashboard/staking/)
- [DefiLlama - Avalanche TVL](https://defillama.com/chain/avalanche)
- [Messari - Avalanche Metrics](https://avalanche.messari.io/network-metrics)

**Burn Data:**
- [Burned AVAX Tracker](https://burnedavax.com/)
- [Avascan - Burned Fees](https://avascan.info/stats/burned-fees/c/all)

**L1 Ecosystem:**
- [Avalanche L1 Explorer](https://subnets.avax.network/stats/network)

**Protocol Updates:**
- [Avalanche Blog](https://www.avax.network/blog)
- [ACPs Repository](https://github.com/avalanche-foundation/ACPs)

#### 2. Use the Template

Copy the most recent snapshot and update all sections:

```bash
# Copy previous snapshot
cp snapshot-2025-11-28.md snapshot-$(date +%Y-%m-%d).md

# Edit the new file, updating:
# - Snapshot date in header
# - All metric values
# - Source links and dates
# - Data freshness table
# - Any new upgrades or developments
```

#### 3. Required Sections

Every snapshot must include:

1. **Token Supply Metrics**
   - Max supply, total supply, circulating supply, staked supply
   - Percentages and calculations

2. **Staking Metrics**
   - Validator count, delegator count, total staked, staking ratio, APR

3. **L1 Ecosystem**
   - Active L1 count, categories, notable projects
   - Validator participation in L1s

4. **Fee Burning Metrics**
   - Total burned, daily burn rate, annual burn rate
   - Recent burn activity trends

5. **Inflation & Emission**
   - Gross inflation, burn offset, net inflation
   - Daily emission, years to max supply

6. **Network Activity**
   - Daily transactions, active addresses, TVL
   - Quarter-over-quarter growth

7. **Recent Upgrades**
   - New upgrades since last snapshot
   - Activation dates and key changes

8. **Data Quality Assessment**
   - Confidence levels for each category
   - Known gaps and limitations
   - Data freshness by category

#### 4. Data Quality Guidelines

**Mark confidence levels:**
- **High Confidence:** Protocol-defined, exchange-reported, blockchain-verified
- **Moderate Confidence:** Third-party analytics, varying sources
- **Low Confidence:** Estimates, incomplete data, API gaps

**Document discrepancies:**
When sources conflict, document:
- The range of values reported
- Which source you selected and why
- The resolution methodology used

**Note data freshness:**
- Fresh: < 6 hours old
- Recent: < 7 days old
- Aging: 7-30 days old
- Stale: > 30 days old

#### 5. Calculation Standards

Use these standard formulas:

```
Staking Ratio = (Staked Supply / Circulating Supply) × 100
Net Inflation = Gross Inflation % - Burn Rate %
Annual Burn % = (Daily Burn × 365 / Total Supply) × 100
% of Max Issued = (Total Supply / 720,000,000) × 100
Daily Emission = (Total Staked × APR) / 365
```

#### 6. Source Citation

Every data point must have:
- **Source:** Organization or platform
- **Link:** Direct URL to data (in Sources section)
- **Date:** When the data was current

Use this format in tables:
```markdown
| Metric | Value | Source | Date |
|--------|-------|--------|------|
| Total Validators | 1,539 | Avascan | Nov 2025 |
```

### Validation Checklist

Before committing a new snapshot, verify:

- [ ] All tables have Source and Date columns filled
- [ ] All calculated values have formulas documented
- [ ] Data quality assessment is complete
- [ ] Discrepancies are documented with resolution
- [ ] Links in Sources section are functional
- [ ] Snapshot date in header is correct
- [ ] Previous snapshot data is preserved (don't modify old snapshots)

## Documents Referencing This Data

The following project documents should reference data snapshots rather than embedding static data:

### Economic Models
- `/home/ygg/Workspace/BCRG/Avalanche/avalanche-research/resources/avalanche/avalanche_economic_model.md`
  - References: Token supply, staking metrics, burn rates, inflation

### Literature Reviews & Analysis
- `/home/ygg/Workspace/BCRG/Avalanche/avalanche-research/resources/avalanche-data/CLAUDE.md`
  - References: Network growth, validator counts, foundation metrics

### Future Documents
When creating new analysis or modeling documents:
1. Link to the relevant snapshot(s)
2. Document which snapshot date you used
3. Note if you made interpolations or adjustments
4. Update references when using newer snapshots

## Data Collection System

### Automated Collection (Snowpeer)

The project includes a Snowpeer API data collection system at:
```
/home/ygg/Workspace/BCRG/Avalanche/avalanche-research/resources/avalanche-data/resources/snowpeer/
```

**Capabilities:**
- Automated collection from Snowpeer API endpoints
- Local SQLite database storage
- Scheduled updates with configurable frequencies
- Data analysis and reporting tools

**Limitations:**
- Validator endpoint returns empty (API gap)
- Delegator endpoint returns empty (API gap)
- No ICM messaging data available
- No LSP data available via API

See `/resources/avalanche-data/resources/snowpeer/DATA_GAPS.md` for details.

### Manual Collection Required

Due to Snowpeer API limitations, these must be collected manually:
- Current validator counts → Use Avascan
- Delegator statistics → Use Avalanche Stats Dashboard
- Real-time staking metrics → Use multiple sources, take consensus
- Market data (price, market cap) → Use CoinGecko/CoinMarketCap
- TVL → Use DefiLlama
- Burn statistics → Use burnedavax.com

### Future Automation

Consider implementing:
1. **Direct RPC queries** to Avalanche nodes for validator/delegation data
2. **Custom blockchain indexer** for precise on-chain metrics
3. **API aggregation** combining multiple data sources
4. **Automated snapshot generation** via scheduled scripts
5. **Data validation** comparing multiple sources automatically

## Snapshot Comparison

To track network evolution, compare metrics across snapshots:

```bash
# Example: Compare staking ratios over time
grep "Staking Ratio" snapshot-2025-11-*.md

# Example: Track validator growth
grep "Total Validators" snapshot-2025-*.md | sort
```

Consider creating analysis scripts to:
- Plot metric evolution over time
- Detect significant changes or anomalies
- Generate trend reports
- Validate data consistency

## Best Practices

### For Analysts

1. **Always check data freshness** before using metrics in critical analysis
2. **Understand confidence levels** and document uncertainty in your work
3. **Use conservative estimates** when data sources conflict
4. **Cite specific snapshots** rather than "current data"
5. **Note when you interpolate** or make assumptions

### For Modelers

1. **Document which snapshot(s)** your model parameters come from
2. **Track sensitivity** to data uncertainty (confidence intervals)
3. **Validate models** against multiple snapshot periods
4. **Update models** when new snapshots reveal material changes
5. **Archive model runs** with snapshot references for reproducibility

### For Researchers

1. **Create new snapshots** before major research milestones
2. **Contribute data sources** when you find better/newer sources
3. **Document methodology** for any derived metrics
4. **Cross-reference** with original protocol documentation
5. **Share findings** that reveal data gaps or inconsistencies

## Troubleshooting

### Data Conflicts

**Problem:** Different sources report different values

**Solution:**
1. Check date of each source (may be from different times)
2. Understand methodology differences (e.g., "active" vs "deployed")
3. Prioritize: Protocol docs > Blockchain explorers > Analytics > News
4. Document the conflict and your resolution in the snapshot

### Missing Data

**Problem:** Required metric not available

**Solution:**
1. Check if Snowpeer API has added new endpoints
2. Query blockchain directly via RPC if possible
3. Use proxy metrics or estimates (clearly documented)
4. Mark as "Not Available" rather than guessing
5. Document the gap in Data Quality Assessment

### Stale Data

**Problem:** Some metrics are weeks/months old

**Solution:**
1. Note staleness in the Data Freshness table
2. Check if the metric changes slowly (e.g., max supply = static)
3. Seek alternative sources for fast-moving metrics
4. Consider direct blockchain queries for critical data
5. Document limitations in your analysis

## Contributing

When contributing to the snapshot system:

1. **Follow the template** structure from existing snapshots
2. **Document your sources** with direct links
3. **Explain calculations** so others can verify
4. **Note data quality** honestly (don't hide gaps)
5. **Preserve history** (don't modify past snapshots)

## Version History

- **2025-11-28:** Initial snapshot system created
  - Established template structure
  - Documented 7 major metric categories
  - Identified Snowpeer API data gaps
  - Created comprehensive November 2025 baseline

## Contact & Support

For questions about the snapshot system:
- Review `/resources/avalanche-data/CLAUDE.md` for project context
- Check `/resources/avalanche-data/resources/snowpeer/README.md` for data collection
- Consult `/resources/avalanche-data/resources/snowpeer/DATA_GAPS.md` for known limitations

---

**Remember:** The goal is consistency and traceability, not perfection. Document what you know, acknowledge what you don't, and always cite your sources.
