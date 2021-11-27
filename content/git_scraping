# Data Scraping

[Simon Willison pioneered a technique that he calls `git scraping`](https://simonwillison.net/2020/Oct/9/git-scraping/). The idea is to use GitHub actions and the `git` commit structure to build time series datasets.

I'm currently building two datasets:
1. In November 2021, CISA announced a [Known Exploited Vulnerabilities Catalog](https://www.cisa.gov/known-exploited-vulnerabilities-catalog). Binding Operational Directive 22-01 uses this as a foundation for requiring federal agencies to patch their systems. Git scraping will enable a couple pieces of analysis: how long does CISA give federal agencies to patch once they know the vulnerability is being exploited? how are these vulnerabilities distributed between different vendors? is there a pattern to how regularly CISA updates the list or requires patching? [Data available here](https://github.com/JosephTLucas/CISA_KNOWN_EXPLOITED_VULNERABILITIES_CATALOG).
2. The [AWS Status Dashboard](https://status.aws.amazon.com). I'm interested in not only the general distribution of outages, but also recovery times and any pattern in cascading failures. [Data available here](https://github.com/JosephTLucas/aws_status).
