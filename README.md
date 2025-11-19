# RingCentral-ZohoDesk-Twilio Integration Server

A Node.js backend service to seamlessly connect RingCentral, Zoho Desk, and Twilio. Automate customer support workflows by handling RingCentral event webhooks, creating/managing Zoho Desk tickets, and sending SMS notifications with Twilio. Designed for support teams to improve response times and unify communications from multiple platforms.

## Features

- **Webhook Processing:** Receives and processes RingCentral webhooks (e.g., missed calls, voicemails).
- **Zoho Desk Integration:** Automatically creates and manages tickets in Zoho Desk based on RingCentral events.
- **Twilio SMS Notifications:** Sends SMS alerts via Twilio for customer communications and ticketing events.
- **Subscription Management:** List, create, renew, update, and delete RingCentral webhook subscriptions.
- **Secure Credentials Handling:** Uses environment variables for API keys and tokens.
- **Database Integration:** Fetches and updates company-specific Zoho Desk configurations from a SQL database.

## Architecture

- **Express.js** server handles all API endpoints.
- **RingCentral SDK** for webhook subscription and event management.
- **Zoho Desk API** for ticket management.
- **Twilio SDK** for sending SMS notifications.
- **MSSQL** for storing and retrieving integration configs.

## Endpoints

### Webhooks
- `POST /api/webhook/send` - Forward events to Zoho Desk server.
- `POST /api/webhook` - Receive and process webhooks from RingCentral.

### RingCentral Subscriptions
- `GET /api/subscription` - List subscriptions.
- `GET /api/subscription/:id` - Get subscription by ID.
- `POST /api/subscription` - Create a new subscription.
- `PUT /api/subscription/:id` - Update a subscription.
- `DELETE /api/subscription/:id` - Delete a subscription.
- `POST /api/subscription/:id/renew` - Renew a subscription.

### Zoho Desk Tickets
- `GET /api/tickets` - List Zoho Desk tickets.
- `POST /api/tickets` - Create a new Zoho Desk ticket.

### Twilio Messaging
- `POST /api/messages` - Send SMS via Twilio.

## Environment Variables

Create a `.env` file at the project root with the following keys:

```env
PORT=3000
COMPANY_ID=<your_company_id>
RC_SERVER_URL=<ringcentral_server_url>
RC_CLIENT_ID=<ringcentral_client_id>
RC_CLIENT_SECRET=<ringcentral_client_secret>
RC_JWT=<ringcentral_jwt_token>
ZOHO_SERVER_URL=<zoho_server_url>
DB_CONNECTION_STRING=<mssql_connection_string>
TWILIO_ACCOUNT_SID=<twilio_account_sid>
TWILIO_AUTH_TOKEN=<twilio_auth_token>
TWILIO_PHONE_NUMBER=<twilio_phone_number>
```

## Installation

```bash
git clone https://github.com/itsronalds/ringcentral-zohodesk-twilio-node-integration.git
cd ringcentral-zohodesk-twilio-node-integration
npm install
cp .env.example .env
# Update your environment variables in .env
```

## Running the Server

```bash
npm start
```

The server will start on the port specified in your `.env` file.

## Usage Example

When a missed call or voicemail event is received from RingCentral, the service:
1. Creates a corresponding ticket in Zoho Desk.
2. Sends a notification via Twilio to the relevant agent or customer.

## References

- [RingCentral Webhook Quick Start](https://developers.ringcentral.com/guide/notifications/webhooks/quick-start)
- [RingCentral API Reference](https://developers.ringcentral.com/api-reference/Subscriptions/listSubscriptions)
- [Twilio Node.js SDK](https://www.twilio.com/docs/libraries/node)
- [Zoho Desk API Docs](https://desk.zoho.com/DeskAPIDocument#Introduction)
- [JavaScript Comments/JSDoc](https://www.aprenderaprogramar.com/index.php?option=com_content&view=article&id=881:guia-de-estilo-javascript-comentarios-proyectos-jsdoc-param-return-extends-ejemplos-cu01192e&catid=78&Itemid=206)
