# Multi-Tenant Voice AI Platform

A comprehensive platform for building and managing voice-powered AI applications with support for multiple tenants and enterprise-grade features.

## Overview

This platform provides end-to-end infrastructure for creating intelligent voice agents that can handle complex conversations across multiple communication channels. Built with scalability and enterprise needs in mind, it supports multi-tenant architecture allowing different organizations to deploy and manage their voice AI solutions independently.

## Key Features

- **Multi-Tenant Architecture**: Isolated environments for different organizations with secure data separation
- **Real-time Voice Processing**: Low-latency speech recognition and synthesis for natural conversations  
- **Flexible Agent Framework**: Configure AI agents with custom personalities, knowledge bases, and workflows
- **Enterprise Integration**: REST APIs and webhooks for seamless integration with existing systems
- **Scalable Infrastructure**: Containerized architecture supporting horizontal scaling
- **Advanced Analytics**: Comprehensive metrics and insights for conversation performance
- **WebSocket Support**: Real-time bidirectional communication for live voice interactions

## Architecture Components

### Core Framework (`voice-agent-framework/`)
- **Agent Management**: Orchestrates conversation flow and agent behavior
- **LLM Integration**: Support for multiple language models (OpenAI, Claude, Llama, etc.)
- **Speech Processing**: Transcription (Deepgram, Whisper) and synthesis (ElevenLabs, AWS Polly, OpenAI TTS)
- **Memory Systems**: Conversation context and knowledge base management
- **Input/Output Handlers**: Flexible interfaces for different communication channels

### Voice Platform (`voice_platform/`)
- Enhanced multi-tenant capabilities
- Advanced agent types (extraction, summarization, knowledge-base agents)
- Improved conversation orchestration
- Enterprise-grade security and isolation

### Local Setup (`local_setup/`)
- Docker-based development environment
- Telephony integration (Twilio)
- Configuration management
- Development tools and utilities

## Getting Started

### Prerequisites
- Docker and Docker Compose V2
- ngrok account for tunneling (development)
- API keys for your chosen providers (LLM, TTS, ASR)

### Quick Setup

1. **Clone and navigate to the project**:
   ```bash
   git clone <repository-url>
   cd multi-tenant-voice-ai-platform/local_setup
   ```

2. **Configure environment**:
   ```bash
   cp .env.sample .env
   # Edit .env with your API keys and configuration
   ```

3. **Start the platform**:
   ```bash
   chmod +x start.sh
   ./start.sh
   ```

   Or manually:
   ```bash
   export DOCKER_BUILDKIT=1
   docker compose build
   docker compose up -d
   ```

## Configuration

### Environment Variables

Create a `.env` file based on `.env.sample` with the following configurations:

#### Speech Recognition
- `DEEPGRAM_AUTH_TOKEN`: For Deepgram transcription services

#### Language Models
- `OPENAI_API_KEY`: OpenAI API access

#### Text-to-Speech
- `ELEVENLABS_API_KEY`: ElevenLabs voice synthesis

#### Telephony
- `TWILIO_ACCOUNT_SID`: Twilio account identifier
- `TWILIO_AUTH_TOKEN`: Twilio authentication token
- `TWILIO_PHONE_NUMBER`: Your Twilio phone number

#### Infrastructure
- `REDIS_URL`: Redis connection for data persistence
- `NGROK_AUTH_TOKEN`: ngrok authentication for tunneling

## API Usage

### Creating an Agent

```bash
curl -X POST http://localhost:8000/agent \
  -H "Content-Type: application/json" \
  -d '{
    "agent_config": {
      "agent_name": "CustomerSupport",
      "agent_type": "conversational",
      "language": "en",
      "max_duration": 300
    },
    "agent_prompts": {
      "system": {
        "role": "You are a helpful customer support agent..."
      }
    }
  }'
```

### Managing Agents

- `GET /agent/{agent_id}` - Retrieve agent configuration
- `PUT /agent/{agent_id}` - Update agent settings  
- `DELETE /agent/{agent_id}` - Remove agent
- `GET /all` - List all agents

### WebSocket Integration

Connect to `ws://localhost:8000/chat/v1/{agent_id}` for real-time voice conversations.

## Supported Providers

### Speech Recognition
- Deepgram


### Language Models  
- OpenAI GPT models

### Text-to-Speech
- ElevenLabs

### Telephony
- Twilio

### Project Structure

```
├── voice-agent-framework/     # Core agent framework
│   ├── agent_manager/        # Agent orchestration
│   ├── agent_types/          # Different agent implementations
│   ├── llms/                 # Language model integrations
│   ├── synthesizer/          # Text-to-speech providers
│   ├── transcriber/          # Speech recognition providers
│   └── helpers/              # Utility functions
├── voice_platform/           # Enhanced platform features
├── local_setup/              # Development environment
│   ├── docker-compose.yml    # Container orchestration
│   ├── telephony_server/     # Telephony integration
│   └── dockerfiles/          # Container definitions
└── requirements.txt          # Python dependencies
```

### Adding New Providers

1. **Speech Recognition**: Extend `transcriber/base_transcriber.py`
2. **Text-to-Speech**: Extend `synthesizer/base_synthesizer.py`
3. **LLM**: Add configuration to `llms/` directory
4. **Telephony**: Create handlers in `input_handlers/telephony_providers/`

### Testing

The platform includes comprehensive testing utilities and example configurations for validation.

## Deployment

### Production Considerations

- Configure secure Redis clustering for multi-tenant data isolation
- Set up load balancing for WebSocket connections
- Implement proper SSL/TLS certificates
- Configure monitoring and logging systems
- Set up backup and disaster recovery procedures

### Scaling

The platform supports horizontal scaling through:
- Container replication
- Database sharding
- Load-balanced WebSocket connections
- Distributed caching strategies

## Security

- Multi-tenant data isolation
- API rate limiting
- Secure credential management
- Input validation and sanitization
- Audit logging for compliance

## Support

For technical support, deployment assistance, or custom development needs, please contact our team or create an issue in the repository.