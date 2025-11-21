# Avo Roadmap Guide

This guide explains how to add and update items in the `avo_roadmap.json` file.

## JSON Structure

The roadmap is a JSON array of items. Each item can have the following properties:

### Required Properties
- `"item"` (string): The name/title of the roadmap item
- `"description"` (string): A detailed description of what the item entails
- `"date"` (string): Due date in format `"YYYY-MM-DD"` (e.g., `"2025-12-25"`)
- `"category"` (string): One of: `"Platform"`, `"Trading"`, `"Community"`, or `"Development"`
- `"completed"` (boolean): `true` or `false`

### Optional Properties
- `"completedDate"` (string): When the item was completed, format `"YYYY-MM-DD"` (only for completed items)
- `"twitterUrl"` (string): Link to Twitter announcement/post
- `"imageUrl"` (string): Link to an image that can be viewed in a lightbox
- `"subItems"` (array): Array of sub-items (see below)

---

## Status Logic

The roadmap automatically determines status based on the `completed` field and `date`:

- **Completed**: `"completed": true`
- **In Progress**: `"completed": false` AND due date is within next 14 days
- **Planned**: `"completed": false` AND due date is more than 14 days away

---

## Examples

### Basic Item (Incomplete)

```json
{
  "item": "Mobile Wallet Integration",
  "description": "Add support for mobile wallet connections including MetaMask Mobile and Trust Wallet.",
  "date": "2025-12-15",
  "category": "Platform",
  "completed": false
}
```

### Completed Item

```json
{
  "item": "Dark Mode Support",
  "description": "Implement dark mode across the entire application.",
  "date": "2025-11-10",
  "category": "Platform",
  "completed": true,
  "completedDate": "2025-11-08"
}
```

### Item with Twitter Link

```json
{
  "item": "NFT Marketplace Launch",
  "description": "Launch the Avo NFT marketplace for trading agent-themed collectibles.",
  "date": "2026-01-20",
  "category": "Platform",
  "completed": true,
  "completedDate": "2026-01-18",
  "twitterUrl": "https://twitter.com/avodotso/status/123456789"
}
```

### Item with Image

```json
{
  "item": "UI Redesign",
  "description": "Complete redesign of the user interface with modern, clean aesthetics.",
  "date": "2026-02-01",
  "category": "Platform",
  "completed": true,
  "completedDate": "2026-01-30",
  "twitterUrl": "https://twitter.com/avodotso/status/123456789",
  "imageUrl": "https://example.com/images/new-ui-preview.png"
}
```

### Item with Sub-Items

```json
{
  "item": "Cross-Chain Support",
  "description": "Enable trading and portfolio management across multiple blockchain networks.",
  "date": "2026-03-01",
  "category": "Platform",
  "completed": false,
  "twitterUrl": "https://twitter.com/avodotso/status/123456789",
  "subItems": [
    {
      "item": "Ethereum Integration",
      "description": "Add support for Ethereum network",
      "date": "2026-02-10",
      "completed": true,
      "completedDate": "2026-02-08"
    },
    {
      "item": "Polygon Integration",
      "description": "Add support for Polygon network",
      "date": "2026-02-20",
      "completed": true,
      "completedDate": "2026-02-19",
      "twitterUrl": "https://twitter.com/avodotso/status/987654321"
    },
    {
      "item": "Arbitrum Integration",
      "description": "Add support for Arbitrum network",
      "date": "2026-03-01",
      "completed": false
    }
  ]
}
```

### Sub-Item with Image and Twitter

```json
{
  "item": "Advanced Analytics Dashboard",
  "description": "Comprehensive analytics dashboard with real-time insights.",
  "date": "2026-04-01",
  "category": "Platform",
  "completed": false,
  "subItems": [
    {
      "item": "Portfolio Performance Graphs",
      "description": "Interactive charts showing portfolio performance over time",
      "date": "2026-03-15",
      "completed": true,
      "completedDate": "2026-03-14",
      "twitterUrl": "https://twitter.com/avodotso/status/111222333",
      "imageUrl": "https://example.com/images/performance-graphs.png"
    },
    {
      "item": "Risk Analysis Tools",
      "description": "Tools to analyze and visualize portfolio risk metrics",
      "date": "2026-03-25",
      "completed": false
    }
  ]
}
```

---

## Full Example JSON File

```json
[
  {
    "item": "Mobile App Launch",
    "description": "Launch native mobile applications for iOS and Android with full trading capabilities.",
    "date": "2025-12-20",
    "category": "Development",
    "completed": false,
    "twitterUrl": "https://twitter.com/avodotso/status/announcement",
    "imageUrl": "https://example.com/mobile-app-preview.png",
    "subItems": [
      {
        "item": "iOS Beta Testing",
        "description": "Complete beta testing phase for iOS app",
        "date": "2025-12-05",
        "completed": true,
        "completedDate": "2025-12-03",
        "twitterUrl": "https://twitter.com/avodotso/status/ios-beta"
      },
      {
        "item": "Android Beta Testing",
        "description": "Complete beta testing phase for Android app",
        "date": "2025-12-10",
        "completed": false
      },
      {
        "item": "App Store Submission",
        "description": "Submit apps to Apple App Store and Google Play Store",
        "date": "2025-12-15",
        "completed": false
      }
    ]
  },
  {
    "item": "Staking Rewards Program",
    "description": "Launch staking program where users can stake AVO tokens to earn rewards.",
    "date": "2026-01-15",
    "category": "Platform",
    "completed": false
  }
]
```

---

## Tips

1. **Always use double quotes** for property names and string values
2. **No trailing commas** - The last item in an array or object should NOT have a comma
3. **Date format**: Always use `"YYYY-MM-DD"` (e.g., `"2025-12-25"`)
4. **Boolean values**: Use `true` or `false` (no quotes)
5. **Optional fields**: If you don't have a value, simply omit the property (don't use `null` or `undefined`)
6. **Categories**: Must be exactly one of: `"Platform"`, `"Trading"`, `"Community"`, or `"Development"`
7. **Sub-items**: Sub-items have the same structure but don't need a `category` field

---

## Validation

After editing, validate your JSON:
1. Use a JSON validator like [JSONLint](https://jsonlint.com/)
2. Make sure all quotes are straight quotes (`"`) not curly quotes (`"` or `"`)
3. Check that all opening `{` and `[` have matching closing `}` and `]`

---

## Updating the Roadmap

1. Edit the `avo_roadmap.json` file in the GitHub repository
2. Commit your changes
3. The website will automatically fetch the latest version (cache-busted with timestamps)
4. Users will see updates when they refresh the page
