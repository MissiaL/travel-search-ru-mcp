<!-- mcp-name: io.github.MissiaL/travel-search-ru-mcp -->

# Travel Search RU MCP

Add travel search to **Claude**, **Codex**, **OpenClaw**, **Hermes**, or any
MCP-compatible AI agent. Find flights, trains, package tours, hotels, and
activities with booking links through **Aviasales**, **Travelata**,
**Level.Travel**, **Tutu.ru**, **Tripster**, and **Sputnik8**.

- Remote Streamable HTTP MCP — no local server to run
- No signup, API key, or authentication required
- Russian city, country, and resort names supported
- Read-only search — booking and payment stay on the provider's website

- **Endpoint:** `https://mcp.botclaw.ru/travel`
- **Version:** `1.5.0`

## Connect

### Claude Desktop

1. Open **Settings → Connectors**.
2. Select **+ → Add custom connector**.
3. Enter `Travel Search RU` as the name.
4. Enter `https://mcp.botclaw.ru/travel` as the URL and save.
5. Enable the connector in a conversation from **+ → Connectors**.

Claude Code:

```bash
claude mcp add --transport http travel-search-ru https://mcp.botclaw.ru/travel
```

### Codex

ChatGPT Desktop and the Codex IDE extension:

1. Open **Settings → MCP servers**.
2. Select **Add server** and choose **Streamable HTTP**.
3. Enter `Travel Search RU` and `https://mcp.botclaw.ru/travel`.
4. Save and restart the client.

Codex CLI:

```bash
codex mcp add travel-search-ru --url https://mcp.botclaw.ru/travel
```

### OpenClaw

Add the server to your OpenClaw configuration:

```json
{
  "mcp": {
    "servers": {
      "travel-search-ru": {
        "url": "https://mcp.botclaw.ru/travel",
        "transport": "streamable-http"
      }
    }
  }
}
```

### Hermes Agent

Add the server to your Hermes MCP configuration:

```yaml
mcp_servers:
  travel-search-ru:
    url: "https://mcp.botclaw.ru/travel"
```

### Other MCP clients

Use the public endpoint with the Streamable HTTP transport:

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

## Try it

After connecting the server, ask your agent:

```text
Find the cheapest dates to fly from Moscow to Istanbul in September.
```

```text
Compare package tours to Turkey for two adults and an 8-year-old child under 250,000 RUB.
```

```text
Plan a week in Rome: flights, a hotel, and activities.
```

```text
Find trains from Moscow to Sochi on September 15 and sort by price.
```

## What it searches

| Category | Sources | What you get |
|---|---|---|
| Flights | Aviasales | Dated offers, passenger-aware search, and a monthly price calendar |
| Trains | Tutu.ru | Cached schedules, indicative carriage fares, and dated result links; verify the selected date and availability on Tutu.ru |
| Package tours | Travelata and Level.Travel | Combined tour results with hotels, meals, dates, and booking links |
| Quick tour shortlists | Travelata | The cheapest current package offers in one fast provider request |
| Hotels | Level.Travel | Hotel-only stays for the requested dates and party |
| Activities | Tripster and Sputnik8 | Excursions, attraction tickets, and transfers from eligible sources |

### Activities

`search_activities` combines Tripster and Sputnik8 results when both sources
support the requested filters. In addition to a city and optional text query,
it accepts optional dates, party size, and a children-friendly filter. Date
filters (`date_from` or `date_to`) and `children_allowed` use Tripster only;
party size alone can use both sources. Sort by `recommended`, `price`,
`rating`, or `reviews`.

Each activity has a normalized `provider`, `price_unit`, and `price_text` so
that the displayed price remains clear for per-person, per-group, or ticket
offers. The server returns results from eligible available sources without
exposing provider errors to the agent.

## Tools

| Tool | Capability |
|---|---|
| `search_flights` | Search flights for specific dates and passenger counts. |
| `get_flight_price_calendar` | Compare flight prices across a month. |
| `search_train_tickets` | Find cached train schedules and indicative fares for a route; verify date and availability through the result link. |
| `search_tours` | Search package tours in Travelata and Level.Travel together. |
| `get_cheapest_travelata_tours` | Get a fast Travelata-only shortlist of the cheapest package tours. |
| `search_hotels` | Search hotels without flights. |
| `get_tour_details` | Refresh a selected offer's price, transfer, and room details. |
| `search_activities` | Find excursions, tickets, and transfers in a city. |
| `list_destinations` | List supported departure cities, countries, and resorts. |

## Safety and privacy

The server searches and compares offers only. It cannot book a trip or take a
payment. Booking and payment happen on the travel provider's website after the
user follows a result link. Prices and availability can change; refresh a
selected package offer before booking and verify the final details on the
provider's website. Tutu.ru train data is not real-time: the requested date is
used in result links but does not filter the upstream timetable, so the train,
seats, and final fare must be checked on Tutu.ru.

Search parameters are sent to Botclaw and the named travel services. They may
include destinations, dates, party size, and children's ages when required for
accurate pricing. Do not include unrelated personal information in search
requests.

## Русский

Travel Search RU MCP добавляет поиск путешествий в Claude, Codex, OpenClaw,
Hermes и другие AI-агенты с поддержкой MCP. Сервер ищет авиабилеты, пакетные
туры, поезда Tutu.ru, отели без перелёта и экскурсии, сравнивает цены и
возвращает ссылки для бронирования. Поддерживаются русские названия городов,
стран, курортов и железнодорожных направлений.
Регистрация, API-ключ и локальный сервер не нужны.

После подключения попробуйте:

```text
Найди самые дешёвые даты для перелёта из Москвы в Стамбул в сентябре.
```

```text
Сравни туры в Турцию для двух взрослых и ребёнка 8 лет до 250 000 ₽.
```

```text
Собери поездку в Рим на неделю: перелёт, отель и экскурсии.
```

Для поездов Tutu.ru сервер возвращает кэшированное расписание и ориентировочные
цены. Выбранная дата используется в ссылке, но не фильтрует само расписание API;
рейс, места и итоговую цену нужно проверить на Tutu.ru.

Сервер выполняет только поиск. Бронирование и оплата происходят на сайте
выбранного сервиса. Параметры поездки передаются Botclaw и перечисленным выше
туристическим сервисам — не добавляйте в запрос лишние персональные данные.

### Экскурсии

`search_activities` объединяет результаты Tripster и Sputnik8, если оба
источника поддерживают выбранные фильтры. Для фильтров `date_from`, `date_to`
или `children_allowed` используется только Tripster; один параметр `persons`
не исключает Sputnik8. Доступна сортировка `recommended`, `price`, `rating` и
`reviews`.

## Support

- Telegram: [@PetrAlexeev](https://t.me/PetrAlexeev)
- Issues: [GitHub Issues](https://github.com/MissiaL/travel-search-ru-mcp/issues)

## License

MIT
