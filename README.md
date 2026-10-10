# Wakizasheye

Wakizasheye is a private, self-hosted web application that its owner uses with their own single eBay UK account. It is not distributed, sold, or offered to anyone else, and it has no public address: it runs on a home server and is reachable only from the owner's home network.

This page exists to describe the application publicly, because the application itself cannot be visited.

## What it does

1. **Search.** The owner searches eBay UK listings by keyword, price range and listing type.
2. **Watch list.** The owner views the items on their own eBay watch list.
3. **Bidding.** For an auction the owner has personally chosen, they enter the most they are willing to pay. The application places that bid on their behalf shortly before the auction ends.
4. **Results.** After the auction ends, the application checks whether the bid won and notifies the owner.

Every bid is for an item the owner selected, at an amount the owner entered. The application does not choose items or prices.

## eBay APIs

| API | Calls | Used for |
|---|---|---|
| Browse API | `item_summary/search`, `get_item_by_legacy_id` | Searching listings and reading an item's current price, bid count and end time |
| Trading API | `GetMyeBayBuying` | Reading the owner's own watch list |
| Buy Offer API | `placeProxyBid`, `getBidding` | Placing the owner's proxy bid and reading the auction result (**access requested**) |

## Status

- Search and watch list are live and in regular use.
- Bidding through the Buy Offer API is built but not in use, because production access to that API has not yet been granted.
- An earlier prototype placed bids through the eBay website instead. That approach is being retired: the purpose of requesting Buy Offer API access is to bid only through eBay's supported API, and the website-based method will be removed once access is granted.

## Usage volume

One user, one eBay account. Total API usage is well under the default limit of 5,000 calls per day, with an expected handful of bids per week.

## Data handling

- The application runs on the owner's own hardware and is not exposed to the internet.
- The owner's eBay OAuth tokens are encrypted at rest.
- It stores only the owner's own bidding records (item ID, title, maximum bid, outcome).
- It does not store personal data about other eBay users.

## Contact

Questions about this application can be raised as an issue on this repository.
