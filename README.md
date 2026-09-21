# Telegram Game V1 — Game Room Vercel Test Console

This is a static Vercel/GitHub frontend for testing the latest Game Room UI against the project's real authoritative Backend 11.16 WebSocket protocol.

## Important architecture note

The canonical backend package contains the authoritative Engine, Backend command execution, and WebSocketGateway, but it does not yet contain a production browser WebSocket transport/authentication server.

Therefore Vercel hosts the UI only. The real backend must be deployed separately on a WebSocket-capable host.

The browser client speaks the canonical envelopes:
- HELLO
- PING
- COMMAND

and consumes:
- CONNECTED
- EVENTS
- COMMAND_RESULT
- ERROR

The frontend does not calculate game outcomes, balances, packet allocation, hand values, settlement, or authoritative timers.

## Vercel

Deploy this folder as a static Vercel project. No build command is required.

Optional URL configuration:

`?ws=wss://YOUR-BACKEND/ws&table=TABLE_ID&player=PLAYER_ID`

Press the backtick (`) key to open the backend connection panel.

## Authentication

Authentication remains a backend responsibility. The deployed browser WebSocket transport must authenticate the player and then call the canonical `WebSocketGateway.connect(connection, auth)` boundary. This HTML does not invent an authentication protocol.
