# kamuicode Workflows

AI content generation workflow templates using Claude Code SDK and kamuicode MCP

## 🌟 Overview

A collection of workflow templates for generating AI content using Claude Code SDK and kamuicode MCP in GitHub Actions. Choose the optimal workflow based on your specific needs.

## 📦 Workflow List

### 🏗️ [Module Workflow](./module-workflow/)
Modularized AI video generation system. Efficiently generates high-quality content through reusable components and multi-agent collaboration.

**⚠️ Note**: Modules may be continuously adjusted for improved reusability and quality.

### 🎵 [Music Video Workflow](./music-video-workflow/)
Automatic music video generation combining audio and video. Google Lyria + Imagen4 + Hailuo-02 Pro integration.

### 📹 [Video Workflow Template](./video-workflow-template/)
Basic video generation workflow. Perfect for learning purposes and simple video creation.

### 🎬 [Video with Background Removal](./video-background-removal-workflow/)
Video generation workflow with background removal functionality.

### 🔍 [Gemini I2V Analysis](./gemini-i2v-workflow/)
Image-to-video generation analysis workflow integrated with Gemini API.

## 🚀 Quick Start

1. **Select a workflow for your use case**
2. **Refer to SETUP.md in the respective folder**
3. **Add required Secrets and MCP configuration**
4. **Run the workflow**

## 📋 Workflow Selection Guide

| Use Case | Recommended Workflow | Features |
|----------|---------------------|----------|
| High-quality, large-scale generation | Module Workflow | Modular, multi-agent |
| Music video creation | Music Video | Audio+video integration |
| Learning, basic use | Video Template | Simple, easy to adopt |
| Background removal needed | Background Removal | Special processing |
| Analysis-focused | Gemini I2V | Gemini integration |

## 🛠️ Requirements

- Claude Code SDK
- kamuicode MCP
- Anthropic API Key
- GitHub Actions

## 🤝 Contributing

We welcome PRs for new workflow templates and bug fixes.

## 📄 License

MIT License

---

🤖 **Powered by [Claude Code SDK](https://docs.anthropic.com/en/docs/claude-code) & kamuicode MCP**