# Fetcher

A powerful web metadata extraction service built with Hono that fetches and parses metadata from any URL.

## Features

- 🚀 **Fast & Lightweight**: Built with Hono for optimal performance
- 🔍 **Comprehensive Metadata Extraction**: Extracts title, description, author, images, and more
- 📱 **Social Media Support**: Extracts Open Graph and Twitter Card metadata
- 🛡️ **Robust Error Handling**: Graceful handling of network errors, timeouts, and invalid URLs
- 🎭 **User Agent Rotation**: Uses random user agents to avoid blocking
- ⚡ **Real-time Processing**: Quick response times with 30-second timeout

## Installation

```bash
npm install @shreyvijayvargiya/fetcher
```

## Usage

### Start the Server

```bash
npm start
# or for development
npm run dev
```

The server will start on port 3002 by default.

### API Endpoint

**POST** `/fetch-metadata`

Extract metadata from a given URL.

#### Request Body

```json
{
	"url": "https://example.com"
}
```

#### Response Format

```json
{
	"success": true,
	"metadata": {
		"url": "https://example.com",
		"title": "Example Website",
		"description": "This is an example website",
		"author": "John Doe",
		"pubDate": "2024-01-01T00:00:00.000Z",
		"image": "https://example.com/image.jpg",
		"robots": "index, follow",
		"keywords": "example, website, demo",
		"language": "en",
		"viewport": "width=device-width, initial-scale=1",
		"charset": "utf-8",
		"themeColor": "#ffffff",
		"favicon": "https://example.com/favicon.ico",
		"openGraph": {
			"og:title": "Example Website",
			"og:description": "This is an example website",
			"og:type": "website"
		},
		"twitterCard": {
			"twitter:card": "summary_large_image",
			"twitter:title": "Example Website"
		},
		"allMetaTags": {
			"description": "This is an example website",
			"keywords": "example, website, demo"
		}
	},
	"timestamp": "2024-01-01T12:00:00.000Z"
}
```

#### Error Responses

The API handles various error scenarios gracefully:

- **Invalid URL**: Returns 400 with validation error
- **Page Not Found (404)**: Returns success with null metadata and 404 status
- **Network Errors**: Returns success with null metadata and error details
- **Server Errors**: Returns success with null metadata and status information

### Example Usage

```javascript
// Using fetch
const response = await fetch("http://localhost:3002/fetch-metadata", {
	method: "POST",
	headers: {
		"Content-Type": "application/json",
	},
	body: JSON.stringify({
		url: "https://github.com",
	}),
});

const data = await response.json();
console.log(data.metadata.title); // "GitHub: Let's build from here"
```

```bash
# Using curl
curl -X POST http://localhost:3002/fetch-metadata \
  -H "Content-Type: application/json" \
  -d '{"url": "https://github.com"}'
```

## Extracted Metadata Fields

| Field         | Description           | Source                                          |
| ------------- | --------------------- | ----------------------------------------------- |
| `title`       | Page title            | `<title>` tag or first `<h1>`                   |
| `description` | Page description      | Meta description, Open Graph, or Twitter Card   |
| `author`      | Content author        | Author meta tags or article author              |
| `pubDate`     | Publication date      | Article published time or date meta tags        |
| `image`       | Main image            | Open Graph image, Twitter image, or first image |
| `robots`      | Robots directive      | Robots meta tag                                 |
| `keywords`    | Page keywords         | Keywords meta tag                               |
| `language`    | Page language         | HTML lang attribute or meta tags                |
| `viewport`    | Viewport settings     | Viewport meta tag                               |
| `charset`     | Character encoding    | Charset meta tag                                |
| `themeColor`  | Theme color           | Theme color meta tag                            |
| `favicon`     | Site favicon          | Favicon link tags                               |
| `openGraph`   | Open Graph metadata   | All `og:*` meta tags                            |
| `twitterCard` | Twitter Card metadata | All `twitter:*` meta tags                       |
| `allMetaTags` | All meta tags         | Complete meta tag collection                    |

## Dependencies

- **Hono**: Fast, lightweight web framework
- **Axios**: HTTP client for fetching web pages
- **Cheerio**: Server-side jQuery implementation for HTML parsing
- **user-agents**: Random user agent generation
- **@hono/node-server**: Node.js server adapter for Hono

## Development

```bash
# Install dependencies
npm install

# Start development server with hot reload
npm run dev

# Start production server
npm start
```

## License

MIT

## Author

**Shrey Vijayvargiya** - [@shreyvijayvargiya](https://github.com/shreyvijayvargiya)

---

Built with ❤️ by [iHateReading](https://github.com/iHateReading)
