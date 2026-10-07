# LURÈVE: Product Requirements Document (reverse-engineered)

This spec was reconstructed from the project's own notes and the custom code, not written before the store. It describes what the store does today. Credentials, customer data, business figures and tracking IDs are left out on purpose.

## 1. Problem statement

Buyers in Pakistan who want a luxury fragrance usually choose between expensive imports and shops they cannot judge online. A new brand has to look credible, explain its fragrances clearly, answer questions quickly and make ordering easy on a phone.

LURÈVE is an online store built for that. It presents ten fragrances as Extrait de Parfum in three sizes, with sets for gifting and sampling, and it handles the questions that usually need a person: what a fragrance smells like, which size to pick, how delivery and returns work.

## 2. Target users

| User | What they need |
|---|---|
| Fragrance buyer in Pakistan | Clear notes and occasions, a trusted look, a fast mobile experience, familiar local payment and delivery |
| Gift buyer | Couple packs, bundles and discovery sets that are easy to choose |
| Owner | A small catalog to manage, order and email that work reliably, and a clear view of cost against price |

## 3. Scope

### 3.1 Implemented

- Store catalog: 40 products in 8 categories. Ten fragrances in 5 ml, 30 ml and 50 ml as separate simple products, plus 10 sets, listed under Bundles, Couple Packs and Discovery Sets. A product can sit in several categories, and Best Sellers is a curated one.
- Shop and category listings that show the 50 ml bottles first and keep the smaller sizes reachable from product pages and sets.
- Product pages with filtering, search and wishlist tools.
- Checkout with local payment gateways, including a buy-now-pay-later option, and a courier integration for delivery.
- Pages: home, about, contact, fragrance guide, FAQ, terms, refunds and returns, blog.
- A fragrance guide with a quick-reference table and a card per fragrance.
- A FAQ with 6 categories and 17 questions, with structured data for search engines.
- 32 blog posts in one category.
- A footer with a newsletter signup, company links and policy links.
- An AI chat concierge that answers from the store's own content.
- A floating WhatsApp chat button.
- SMTP email delivery for orders and contact forms.
- Ad and analytics tracking, including a fix so add-to-cart events fire on product pages.
- SEO setup with structured data and faster indexing support.
- Performance work: caching, image optimization, a Redis object cache and a preloaded hero image.
- An internal cost audit tool that compares landed cost with price and margin for every product.
- A barcode utility for product labels.

### 3.2 Partial or open

- Image alt text is missing on a little over half the images.
- Render-blocking theme CSS is not resolved.
- Footer social links are placeholders, and the About page still shows stock images.
- A category name has a typo.
- The chatbot has no usage or cost monitoring.
- The local copy of the site is not synced with the live server, and there is no staging site.

### 3.3 Out of scope

- International shipping (Pakistan only)
- A skincare line (part of the brand vision, not live)
- Automated tests
- A custom theme from scratch (a commercial theme with a child theme is used)

## 4. Key flows

### 4.1 Choose and buy a fragrance
1. The visitor lands on the home page or a blog post and finds a fragrance through the shop, search, filters or the fragrance guide.
2. The product page shows the notes, the sizes and the price.
3. The visitor adds a bottle or a set to the cart and checks out with a local gateway, or a buy-now-pay-later option.
4. The courier integration carries the order to delivery, and email confirms it.

### 4.2 Get an answer without waiting
1. The visitor opens the FAQ or asks the concierge chatbot.
2. The chatbot searches the store's own content and answers. A WhatsApp button is always visible for a person.

### 4.3 Discover through content
1. A search brings the visitor to a blog post, such as a buying guide for a fragrance style.
2. The post links to the fragrance guide and to the product pages.

### 4.4 Owner reviews costs
1. The owner opens the cost audit in the admin area.
2. Each product shows landed cost, price and margin, so pricing and set composition can be adjusted.

### 4.5 A larger page ships
1. A design spec and an implementation plan are written.
2. The page is built and checked, the cache is cleared and the result is reviewed.

## 5. Non-functional characteristics

- **Performance.** Mobile PageSpeed 85 and desktop 98, up from 48 on mobile.
- **Hosting.** One VPS with nginx, PHP and Redis, behind Cloudflare.
- **Tracking.** Meta, TikTok and Google pixels and listings feeds.
- **Maintenance.** Many third-party plugins, so updates and compatibility need regular attention.
- **Testing.** Manual checks only.

## 6. Risks

| Risk | Detail | Effect |
|---|---|---|
| Content only in the database | Pages and posts are not in version control | A bad edit or lost backup is hard to undo |
| No staging site | Changes are made on the live store | A mistake is visible to customers at once |
| Many third-party plugins | Updates, licences and compatibility need ongoing management | Breakage after an update, security exposure |
| Unsynced local copy | The local files differ from the live ones | Confusion about which version is current |
| Unmonitored AI cost | The chatbot has no usage tracking | Surprise bills |
| Launch-phase brand | Few reviews and little traffic history | Trust and conversion rely on content and design |

## 7. Open questions

- Which sync or deploy path should connect the local files and the live server?
- Should a staging site be added?
- When will the placeholder footer links and stock images be replaced?
- Should skincare become a live line?
