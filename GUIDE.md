# Avo Roadmap Guide

This guide explains how to add and update items in the `avo_roadmap.json` file.

## JSON Structure

The roadmap is a JSON object containing metadata and an array of roadmap items.

### Root Level Properties

- `"updated_at"` (string): Date when the roadmap was last updated, format `"YYYY-MM-DD"` (e.g., `"2025-11-20"`)
- `"version"` (string): Version of the roadmap structure (e.g., `"1.0"`)
- `"items"` (array): Array of roadmap items (see below)

### Roadmap Item Properties

Each item in the `items` array can have the following properties:

### Required Properties
- `"item"` (string): The name/title of the roadmap item
- `"description"` (string): A detailed description of what the item entails
- `"date"` (string): Due date in format `"YYYY-MM-DD"` (e.g., `"2025-12-25"`)
- `"category"` (string): One of: `"Platform"`, `"Trading"`, `"Community"`, or `"Development"`
- `"completed"` (boolean): `true` or `false`

### Optional Properties
- `"completedDate"` (string): When the item was completed, format `"YYYY-MM-DD"` (only for completed items)
- `"tentative"` (boolean): Set to `true` if the deadline is tentative and may change
- `"tentativeReason"` (string): Explanation for why the deadline is tentative (required if `tentative` is `true`)
- `"twitterUrl"` (string): Link to Twitter announcement/post
- `"imageUrl"` (string): Link to an image that can be viewed in a lightbox
- `"signed_by"` (string): Name or identifier of the person who signed off on or is responsible for this item (only for top-level items, not sub-items)
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

### Tentative Item

```json
{
  "item": "Beta Version Release",
  "description": "Expand the mobile app release to a larger test group with an initial controlled public beta.",
  "date": "2025-11-22",
  "tentative": true,
  "tentativeReason": "Timeline depends on successful completion of Apple Developer Account approval and TestFlight setup. Beta launch will proceed once all app store compliance requirements are met.",
  "category": "Development",
  "completed": false
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

### Item with Signed By

```json
{
  "item": "Security Audit",
  "description": "Complete comprehensive security audit of all smart contracts and infrastructure.",
  "date": "2026-02-15",
  "category": "Development",
  "completed": false,
  "signed_by": "John Doe"
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
{
  "updated_at": "2025-11-20",
  "version": "1.0",
  "items": [
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
}
```

---

## Tips

1. **Always update the `updated_at` field** - When making any changes to the roadmap, update the `"updated_at"` field at the root level to the current date
2. **Always use double quotes** for property names and string values
3. **No trailing commas** - The last item in an array or object should NOT have a comma
4. **Date format**: Always use `"YYYY-MM-DD"` (e.g., `"2025-12-25"`)
5. **Boolean values**: Use `true` or `false` (no quotes)
6. **Optional fields**: If you don't have a value, simply omit the property (don't use `null` or `undefined`)
7. **Categories**: Must be exactly one of: `"Platform"`, `"Trading"`, `"Community"`, or `"Development"`
8. **Sub-items**: Sub-items have the same structure but don't need a `category` field and cannot have a `signed_by` field
9. **Tentative deadlines**: Use `"tentative": true` for dates that may change due to dependencies. Always include a `"tentativeReason"` explaining why (e.g., pending approvals, dependent on other items, external factors)
10. **Signed by**: The `"signed_by"` field is only available for top-level items to track accountability. Sub-items inherit the responsibility from their parent item

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

---

## Recent Status Notes

- Burn Mechanism Infrastructure Review completed: 2025-11-23 (signed by codex)
