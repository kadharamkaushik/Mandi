# ADR-0007: Tiered store connectors

Status: accepted · Date: 2026-09-27

## Decision

Every store implements one StoreConnector interface; a capability record per store (and per user link) decides tier A, B or C at runtime.

## Why

Store API access will change over time (Instamart approval, Blinkit partnership). A capability switch avoids app releases and lets the router fall back to tier C if an API fails or access is revoked.

## Consequences

Zepto and Instamart connectors use the official MCP servers through @modelcontextprotocol/sdk; unofficial wrappers and logged-in scraping are prohibited.
