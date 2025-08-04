# kamuicode Workflows

AI content generation workflow collection leveraging Claude Code SDK and kamuicode MCP

## 🌟 Overview

A collection of workflow templates for generating AI content using Claude Code SDK and kamuicode MCP in GitHub Actions. Choose the optimal workflow according to your specific purpose.

**🆕 v0.6.0 Latest Features**: Autonomous banner generation system has been added. Professional banner generation workflow with AI quality assurance functionality. Achieves automatic commercial-grade quality through Gemini Vision API's rigorous evaluation system (1-100 point scoring) and 70-point pass criteria.

## 📦 Workflow List

### 🏗️ [Module Workflow](./module-workflow/) 🆕 v0.6.0
Modularized AI article, video, banner, and news generation system. Efficiently generates high-quality content through reusable components and multi-agent collaboration.

**🆕 Latest Features (v0.6.0-autonomous-banner):**
- **🎨 Autonomous Banner Generation**: Professional banner generation with AI quality assurance
- **🔍 Gemini Vision Evaluation**: Rigorous 1-100 point scoring system (70-point pass criteria)
- **⚙️ Auto-Improvement Function**: Automatic prompt adjustment and image post-processing based on evaluation results
- **🖼️ ImageMagick & FFmpeg Integration**: Technical solutions for quality issues that AI generation alone cannot solve
- **📊 Up to 5 Iterations**: Automatically repeat improvements until quality standards are met
- **📋 Detailed Documentation**: Banner evaluation criteria, service specifications, etc. (470 lines added)
- **🔧 Image Processing Expansion**: FFmpeg & ImageMagick usage guides (1,026 lines added)

**Continued Features (v0.5.0-):**
- **🎤 MiniMax Voice Design**: High-quality Japanese voice generation & character voice support
- **👄 Pixverse Lipsync**: High-quality lipsync with constraint handling (5MB/30sec)
- **📤 FAL Upload**: Automatic FAL URL conversion for local files
- **🎞️ Video Integration**: FFmpeg-powered video concatenation & subtitle overlay
- **🔧 Claude Code SDK Integration**: Migration to more stable CCSDK foundation

**Continued Features (v0.4.0-):**
- **📰 AI News Article Generation**: Complete automation from web search → fact-checked articles → audio
- **🔧 Git Push Conflict Avoidance**: 95% success rate system with 3 retries across all 33 modules
- **🌐 Fiction Prevention**: High-quality article creation without any fictional information

**Continued Features (v0.3.0-):**
- **📺 News Video**: Complete automatic production of professional news programs
- **🎵 Audio & Lipsync**: High-quality narration + lipsync synchronization
- **📝 Subtitle System**: Accurate subtitle timing analysis & generation
- **🎬 ffmpeg Integration**: Professional-level video editing (subtitles, title frames)

**Continued Features (v0.2.0-):**
- **Multi-model Support**: Free selection from 5 image types & 3 video types
- **t2v/i2v/r2v Integration**: Text-to-video, image-to-video, reference video generation
- **Dynamic Model Selection**: Automatic tool detection from kamuicode-usage.md
- **Model Optimization**: Auto-generated prompts tailored to each AI model's characteristics

**Key Features:**
- **🎨 Autonomous Banner Generation**: Professional banner generation with AI quality assurance
- **🔍 AI Quality Evaluation**: Rigorous 1-100 point scoring system using Gemini Vision API
- **⚙️ Auto-Improvement**: Automatic prompt adjustment and image post-processing based on evaluation results
- **🎤 High-Quality Audio Generation**: MiniMax Voice Design & multi-model support
- **👄 Constraint-Aware Lipsync**: Complete handling of strict constraints like Pixverse
- **📤 FAL Upload**: Automatic URL conversion for video, image, and audio files
- **🎞️ Video Integration**: FFmpeg-powered concatenation, subtitle, and analysis functions
- **📺 News Video**: Integrated AI announcer, audio, subtitles, and titles
- **Video Generation**: High-quality video production with any AI model combination
- **15 Orchestrators**: Optimal workflow selection for different use cases

**⚠️ Note**: Modules may be continuously adjusted for improved reusability and quality.

### 🎵 [Music Video Workflow](./music-video-workflow/)
Automatic music video generation integrating audio and video. Combination of Google Lyria + Imagen4 + Hailuo-02 Pro.

### 📹 [Video Workflow Template](./video-workflow-template/)
Basic video generation workflow. Perfect for learning purposes and simple video creation.

### 🎬 [Video with Background Removal](./video-background-removal-workflow/)
Video generation workflow including background removal functionality.

### 🔍 [Gemini I2V Analysis](./gemini-i2v-workflow/)
Image-to-video generation analysis workflow integrated with Gemini API.

## 🚀 Quick Start

1. **Select a workflow that matches your use case**
2. **Refer to SETUP.md in the respective folder**
3. **Add required Secrets and MCP configuration**
4. **Execute the workflow**

## 📋 Workflow Selection Guide

| Use Case | Recommended Workflow | Features |
|----------|---------------------|----------|
| 🆕 Autonomous banner generation | Module Workflow (Autonomous Banner) | AI quality assurance, 70-point pass criteria |
| 🆕 AI news article creation | Module Workflow (AI News Article) | Web search → fact-checked articles → audio generation |
| 🆕 News program production | Module Workflow (News Video) | AI announcer, audio, subtitles, title integration |
| 🆕 Multi-model video generation | Module Workflow (Multi-Model) | Any AI model selection, t2v/i2v/r2v support |
| High-quality, large-scale generation | Module Workflow | Modular, multi-agent |
| Banner advertisement creation | Module Workflow (Banner) | Auto-generate up to 4 banners from concept |
| Music video creation | Music Video | Audio+video integration |
| Learning, basic use | Video Template | Simple, easy to adopt |
| Background removal needed | Background Removal | Special processing |
| Analysis-focused | Gemini I2V | Gemini integration |

## 🛠️ Requirements

- **Claude Code SDK**: AI agent execution environment
- **kamuicode MCP**: Image, video, audio, lipsync generation services (multi-model support)
- **Anthropic API Key**: Claude AI access
- **Gemini API Key**: Image evaluation & quality assessment + Gemini Vision analysis (required) 🆕
- **FAL_KEY**: FAL API Key (create account and obtain API key)
- **GitHub Actions**: Workflow execution environment
- **GitHub PAT Token**: Pull request creation
- **ffmpeg**: Professional-level video editing (used for news video, subtitles, concatenation)
- **ImageMagick**: Advanced image post-processing (used for autonomous banner generation) 🆕

### 🆕 v0.6.0 Support Status
- **Autonomous Banner Generation**: Professional banner generation with AI quality assurance
- **Gemini Vision Evaluation**: Rigorous 1-100 point scoring system (70-point pass criteria)
- **Auto-Improvement Function**: Automatic prompt adjustment and image post-processing based on evaluation results
- **ImageMagick & FFmpeg Integration**: Technical solutions for quality issues that AI generation alone cannot solve
- **Up to 5 Iterations**: Automatically repeat improvements until quality standards are met
- **Detailed Documentation Enhancement**: Banner evaluation criteria, service specifications, etc. (470 lines added)
- **Image Processing Expansion**: FFmpeg & ImageMagick usage guides (1,026 lines added)

### Continued Support (v0.5.0-)
- **Advanced Workflow Integration**: Audio generation, lipsync, video concatenation, FAL upload integration
- **MiniMax Voice Design**: High-quality Japanese voice & character voice support
- **Pixverse Constraint Handling**: Strict constraint checking for 5MB video/30sec audio
- **Claude Code SDK Integration**: Migration to more stable CCSDK foundation
- **FFmpeg Enhancement**: Video concatenation, subtitle overlay, audio analysis functions

### Continued Support (v0.4.0-)
- **AI News Articles**: Complete automation from web search → article creation → audio generation
- **Git Push Conflict Avoidance**: 95%+ success rate across all 33 modules
- **Fiction Prevention**: High-reliability system with fact-checked articles only
- **High-Reliability System**: Stable operation with 3 retries and random waiting

### Continued Support (v0.3.0-)
- **Multi-Model**: Support for 5 image types, 3 video types, audio, and lipsync
- **ffmpeg Integration**: Professional video editing capabilities
- **Gemini Vision**: High-precision lipsync analysis
- **Multi-Language Support**: Automatic translation functionality

## 🤝 Contributing

We welcome PRs for new workflow templates and bug fixes.

## 📄 License

MIT License

---

🤖 **Powered by [Claude Code SDK](https://docs.anthropic.com/en/docs/claude-code) & kamuicode MCP**