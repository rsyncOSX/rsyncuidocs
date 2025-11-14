+++
author = "Thomas Evensen"
date = "2025-01-30"
title =  "Latest version of rsync"
tags = ["rsync version"]
categories = ["general information"]
lastmod = "2024-09-10"
+++

The default `/usr/bin/rsync` differs between macOS versions:

- **macOS Sonoma**: Uses rsync version 2.6.9 (released November 2006)
- **macOS Sequoia and Tahoe**: Use `openrsync`, a BSD-licensed implementation compatible with rsync protocol 29 and version 2.6.9

{{< alert color="warning" >}}

I strongly recommend installing the latest version of rsync (version 3.x) to take full advantage of RsyncUI's features.

{{< /alert >}}

### Installing rsync via Homebrew

Install the latest version using Homebrew:
```bash
brew install rsync
```

After installation, configure RsyncUI:

1. Navigate to Settings and select *Rsync and path*
2. Enable *Rsync ver3.x*
3. RsyncUI will automatically set the correct path

**Note:** RsyncUI's snapshot and sync remote features require rsync version 3.x due to limitations in version 2.6.9.