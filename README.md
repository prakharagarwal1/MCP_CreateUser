# MCP Server and Client

A Model Context Protocol (MCP) server with a `create-user` tool that persists users to a local JSON file, plus a client for testing it.

## Overview

This project demonstrates a minimal MCP server built with the
[`@modelcontextprotocol/sdk`](https://github.com/modelcontextprotocol/typescript-sdk)
package. It exposes a single tool — `create-user` — that accepts a name, email,
address, and phone, then appends the record to `data/users.json`.

## Project Structure

```
.
├── index.js            # MCP server entry point
├── package.json        # Scripts and dependencies
├── package-lock.json
├── .gitignore
├── README.md
└── data/
    └── users.json      # Persistent user store (created on first run)
```

## Prerequisites

- Node.js 18+
- npm

## Setup

```bash
npm install
```

## Running the Server

Start the server in STDIO mode (the transport used by MCP clients and the
Inspector):

```bash
npm run server:dev
```

## Running the Inspector

The MCP Inspector lets you list and call tools from a web UI:

```bash
npm run server:inspect
```

It opens `http://127.0.0.1:6274` automatically. Set `Transport Type` to `STDIO`,
`Command` to `npm`, and `Arguments` to `run server:dev`, then click
**Connect**.

## Tools

### `create-user`

Create a new user in the database.

**Parameters**

| Name    | Type   | Required | Description           |
| ------- | ------ | -------- | --------------------- |
| name    | string | yes      | Full name of the user |
| email   | string | yes      | Email address         |
| address | string | yes      | Postal address        |
| phone   | string | yes      | Phone number          |

**Example call**

```json
{
  "name": "Alice",
  "email": "alice@example.com",
  "address": "123 Main St",
  "phone": "555-1234"
}
```

**Result**

```json
{
  "content": [
    {
      "type": "text",
      "text": "User 5 created successfully"
    }
  ]
}
```

Users are stored in `data/users.json` as an array of objects with an auto-incrementing
`id`.

## License

ISC
