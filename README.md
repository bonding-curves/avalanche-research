# Avalanche Economic Research Portal

A comprehensive economic analysis of the Avalanche network by the Bonding Curve Research Group (BCRG), built with [Quartz v4](https://quartz.jzhao.xyz/).

## Overview

This research portal presents a systematic analysis of Avalanche's economic dynamics, progressing from foundational concepts through advanced mathematical specifications. The work applies rigorous analytical frameworks—from traditional economic theory to control systems engineering—to decode the complex interactions that drive network behavior.

### Research Milestones

1. **Milestone 1: Foundational Taxonomies**
   - Participant Roles Taxonomy
   - Economic Taxonomy
   - Mechanism Taxonomy
   - Avalanche Economy relative to the Open Economy

2. **Milestone 2: Systems Engineering**
   - Model-Based Systems Engineering Perspective
   - Subsystem Analysis and MultiGraph Model
   - ACP (Avalanche Community Proposals) Summaries

3. **Milestone 3: Mathematical Specification**
   - Differential Specification using control theory

4. **Milestone 4: Practical Applications**
   - Economic Hypotheses and testable predictions

## Running Locally

### Prerequisites

- Node.js 18.14+ (check with `node -v`)
- npm 9.3.1+ (check with `npm -v`)

### Installation

1. Clone the repository:
```bash
git clone https://github.com/bonding-curves/avalanche-research.git
cd avalanche-research
```

2. Install dependencies:
```bash
npm install
```

### Development Server

Run the local development server:
```bash
npx quartz build --serve
```

The site will be available at `http://localhost:8080`

For custom port configuration:
```bash
npx quartz build --serve --port 3000
```

If you encounter WebSocket issues, specify a different WebSocket port:
```bash
npx quartz build --serve --port 8080 --wsPort 3002
```

### Building for Production

To build the static site for deployment:
```bash
npx quartz build
```

The built files will be in the `public/` directory.

## Project Structure

```
avalanche-research/
├── content/           # Markdown content files
│   ├── index.md      # Homepage
│   ├── about/        # About pages
│   ├── milestone1/   # Foundational taxonomies
│   ├── milestone2/   # Systems engineering analysis
│   ├── milestone3/   # Mathematical specifications
│   └── milestone4/   # Economic hypotheses
├── quartz/           # Quartz framework files
│   └── static/       # Static assets (images, etc.)
├── public/           # Built site (generated)
└── quartz.config.ts  # Site configuration
```

## Adding/Editing Content

1. Edit markdown files in the `content/` directory
2. The development server will automatically rebuild and refresh
3. Use standard markdown with support for:
   - LaTeX math equations (enclosed in `$` or `$$`)
   - Internal links using `[[filename]]` or `[text](path)`
   - Tables, code blocks, and other GitHub-flavored markdown

## Configuration

Site configuration is in `quartz.config.ts`. Key settings:
- Site title and description
- Base URL for deployment
- Theme and appearance options
- Plugin configurations

## Deployment

This site can be deployed to:
- GitHub Pages (see [Quartz hosting docs](https://quartz.jzhao.xyz/hosting))
- Netlify, Vercel, or other static hosting services
- Any web server that can serve static files

## About BCRG

The Bonding Curve Research Group (BCRG) is an independent, decentralized collective of scholars, engineers, and researchers dedicated to the comprehensive study of bonding curves and blockchain economics. This Avalanche research demonstrates our analytical capabilities in understanding complex economic systems.

### Links

- [BCRG Library](https://bonding-curve-research-group.gitbook.io/bonding-curve-research-group-library)
- [Our Research](https://mirror.xyz/0x8fF6Fe58b468B1F18d2C54e2B0870b4e847C730d)
- [GitHub](https://github.com/bonding-curves)
- [Twitter](https://twitter.com/Bonding_Curves)

## Contributing

For questions, suggestions, or contributions to the research, please:
1. Open an issue on GitHub
2. Contact BCRG through our official channels
3. Submit a pull request with proposed changes

## License

This research is published openly for community benefit. Please cite appropriately when referencing this work.

---

Built with [Quartz v4](https://quartz.jzhao.xyz/) by [Jacky Zhao](https://jzhao.xyz/)