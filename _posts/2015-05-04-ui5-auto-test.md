---
layout: post
title: Node.js
---

# Setup npm-based Automation Infrastructure with Karma

## Installation Steps - Globally

Set environment variables in the command line.

```bash
setx HTTP_PROXY http://proxy:8080
setx HTTPS_PROXY http://proxy:8080
setx FTP_PROXY http://proxy:8080
setx NO_PROXY localhost,127.0.0.1,.sap.corp
```

Update and install the package managers and runner globally

```bash
npm update -g npm
npm install -g bower
npm install -g grunt-cli
npm install -g karma-cli
```

## Installation Steps - Per Project

Install project dependent packages using the following commands

```bash
npm install
bower install
```
