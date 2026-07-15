<!-- mcp-name: io.github.MissiaL/travel-search-ru-mcp -->

# Travel Search RU MCP

Remote MCP server for travel search through **Aviasales**, **Travelata**,
**Level.Travel**, and **Sputnik8**. It finds flights, package tours, hotels, and
activities with current prices and booking links. Russian city, country, and
resort names are supported. No API key or local server installation is required.

## Connect

- Endpoint: `https://mcp.botclaw.ru/travel`
- Transport: Streamable HTTP
- Authentication: none
- Version: `1.0.0`

Claude Code:

```bash
claude mcp add --transport http travel-search-ru https://mcp.botclaw.ru/travel
```

JSON configuration:

```json
{
  "mcpServers": {
    "travel-search-ru": {
      "type": "streamable-http",
      "url": "https://mcp.botclaw.ru/travel"
    }
  }
}
```

## Tools

| Tool | Capability |
|---|---|
| `search_flights` | Search flights for specific dates and passenger counts. |
| `get_flight_price_calendar` | Compare flight prices across a month. |
| `search_tours` | Search package tours in Travelata and Level.Travel together. |
| `search_hotels` | Search hotels without flights. |
| `get_tour_details` | Refresh a selected offer's price, transfer, and room details. |
| `search_activities` | Find excursions, tickets, and transfers in a city. |
| `list_destinations` | List supported departure cities, countries, and resorts. |

## Safety and privacy

The server searches and compares offers only. Booking and payment happen on the
travel provider's website after the user follows a result link.

Travel search parameters are sent to Botclaw and the named travel services. They
may include destinations, dates, party size, and children's ages when required for
accurate pricing. Do not include unrelated personal information in search requests.

## Русский

Travel Search RU MCP помогает искать путешествия через **Aviasales**,
**Travelata**, **Level.Travel** и **Sputnik8**. Сервер находит авиабилеты,
пакетные туры, отели без перелёта и экскурсии, сравнивает цены и возвращает
ссылки для бронирования. Поддерживаются русские названия городов, стран и
курортов. API-ключ и локальная установка сервера не требуются.

Сервер выполняет только поиск. Бронирование и оплата происходят на сайте
выбранного сервиса. Параметры поездки передаются Botclaw и перечисленным выше
туристическим сервисам — не добавляйте в запрос лишние персональные данные.

## Support

- Telegram: [@PetrAlexeev](https://t.me/PetrAlexeev)
- Issues: [GitHub Issues](https://github.com/MissiaL/travel-search-ru-mcp/issues)

## License

MIT
