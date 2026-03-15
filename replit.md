# Discord Server Copy Bot

## Overview

This is a Discord bot application designed to automate server copying/cloning operations with a monetization system. The bot provides a ticket-based interface for users to purchase and execute server copy operations, integrated with ProBot for payment processing. It includes activity status updates showing member count and comprehensive logging of all operations.

## Recent Changes (October 14, 2025)

- **Improved Copy Progress Display**: Changed copy progress to use a single message that updates instead of multiple messages
- **Limited Emoji Copying**: Restricted emoji copying to maximum 10 emojis to improve performance
- **Cleaner Interface**: Removed duplicate status messages, now shows only progress bar updates

## Previous Changes (October 11, 2025)

- **Removed Voice Channel Feature**: Removed automatic voice channel joining functionality and related configuration
- **Cleaned Up Code**: Removed @discordjs/voice dependency and voiceChannelId from configuration

## Previous Changes (October 9, 2025)

Added features to enhance bot functionality:
- **Streaming Status**: Bot displays streaming activity showing real-time server member count
- **Purchase Logging**: Green embed messages posted to purchase operations channel (1425571394887876690) with member name, price, duration in seconds, and copy types
- **Operation Logging**: Detailed logs posted to logs channel (1425571594826420366) with copier name, source/destination servers, and duration in minutes
- **Enhanced Copy Messages**: Improved "copying in progress" message with professional styling, removed DM functionality

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Core Technologies
- **Runtime**: Node.js 16.x
- **Primary Framework**: Discord.js v13.17.1 (standard bot client)
- **Secondary Framework**: discord.js-selfbot-v13 (for advanced automation)
- **Database**: wio.db (JSON-based file storage)

### Application Structure

**Bot Client Architecture**
- Single main client instance with full intents (3276799) for comprehensive Discord API access
- Dual-client pattern: Main bot client + selfbot client for extended capabilities
- Slash command system using Discord's native command registration

**Data Persistence**
- JSON file-based storage using wio.db library
- Three data files:
  - `DataBase.json`: Main application data
  - `tickets.json`: Ticket counter and tracking
  - `settings.json`: Panel channel and category configuration
- No relational database - all data stored as JSON objects

**Feature Modules**

1. **Ticket System**: Slash command `/setup` creates support panels where users can open tickets for server copy requests
2. **Payment Integration**: ProBot integration for credit-based payment processing
3. **Server Cloning**: Automated Discord server replication functionality
4. **Activity Monitoring**: Real-time member count display in bot status
5. **Cooldown System**: Multiple cooldown maps prevent command spam

### Configuration Management

Centralized configuration in `config.js`:
- ProBot user IDs for payment verification
- Payment recipient ID for credit transfers
- Server copy pricing
- Target server ID
- Bot authentication token
- Channel IDs for purchase logs and general logs

All sensitive data (tokens, IDs) externalized to config file for security and easy deployment.

### Design Patterns

**Event-Driven Architecture**: Bot responds to Discord events (ready, messageCreate, interactionCreate, etc.)

**Cooldown Pattern**: Map-based cooldown tracking (`cooldowns`, `cooldowns1`, `cooldowns2`) prevents abuse

**Modular Channel Management**: Separate channels for different log types (purchases, operations, errors)

**State Persistence**: Ticket counter maintains state across restarts via JSON storage

## External Dependencies

### Discord APIs
- **Discord.js v13**: Main bot framework for Discord Bot API
- **discord.js-selfbot-v13**: Extended automation capabilities (user-like actions)

### Payment & Verification
- **ProBot**: Third-party Discord bot for credit system and payment processing
- **2captcha**: CAPTCHA solving service integration
- **node-capmonster**: Alternative CAPTCHA solving service

### Utilities
- **wio.db**: JSON-based database for persistent storage
- **debug**: Debug logging utility
- **fs**: Native Node.js file system for JSON operations

### Infrastructure Requirements
- Discord Bot Token (standard bot account)
- Discord Server with specific channel IDs configured
- ProBot bot present in server for payment processing
- Multiple text channels for logging operations