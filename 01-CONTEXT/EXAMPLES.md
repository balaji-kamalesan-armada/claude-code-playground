# Context Examples

## Example 1: Code Without Context ❌

**File: `bad-example.js`**
```javascript
// WITHOUT CONTEXT - Hard to understand

function calc(p, t) {
  let d = 0;
  if (t === 'p') d = p * 0.2;
  if (t === 'e') d = p * 0.4;
  return p - d;
}

function ship(t) {
  return t > 50 ? 0 : 10;
}

function proc(u, items) {
  let t = 0;
  for (let i of items) {
    t += i.p * i.q;
  }
  let d = calc(t, u.t);
  let s = ship(t);
  return t - d + s;
}

module.exports = { calc, ship, proc };
```

**Problems:**
- Cryptic function names (`calc`, `ship`, `proc`)
- Single-letter variables (`p`, `t`, `d`, `s`, `u`, `i`)
- No comments
- No documentation
- Hard to understand what this does

---

## Example 2: Code With Context ✅

**File: `good-example.js`**
```javascript
// WITH CONTEXT - Easy to understand

/**
 * Calculate discount based on user tier
 * Business Rules:
 * - Premium users: 20% discount
 * - Enterprise users: 40% discount
 * - Standard users: 0% discount
 *
 * @param {number} price - Base price in USD
 * @param {string} tier - User tier: 'standard', 'premium', or 'enterprise'
 * @returns {number} Discount amount in USD
 */
function calculateDiscount(price, tier) {
  let discount = 0;

  // Premium users get 20% discount
  if (tier === 'premium') {
    discount = price * 0.2;
  }

  // Enterprise users get 40% discount
  if (tier === 'enterprise') {
    discount = price * 0.4;
  }

  return discount;
}

/**
 * Calculate shipping cost
 * Business Rule: Free shipping on orders over $50
 *
 * @param {number} totalPrice - Total order price in USD
 * @returns {number} Shipping cost in USD (0 if free, 10 if standard)
 */
function calculateShipping(totalPrice) {
  const FREE_SHIPPING_THRESHOLD = 50;
  const STANDARD_SHIPPING_COST = 10;

  // Free shipping for orders over $50
  return totalPrice > FREE_SHIPPING_THRESHOLD ? 0 : STANDARD_SHIPPING_COST;
}

/**
 * Process order and calculate final price
 * Final price = (items total - discount) + shipping
 *
 * @param {Object} user - User object with tier property
 * @param {Array} items - Array of items with price and quantity
 * @returns {number} Final order price in USD
 */
function processOrder(user, items) {
  // Calculate total price of all items
  let itemsTotal = 0;
  for (let item of items) {
    itemsTotal += item.price * item.quantity;
  }

  // Apply tier-based discount
  const discount = calculateDiscount(itemsTotal, user.tier);

  // Calculate shipping (based on items total, not discounted price)
  const shipping = calculateShipping(itemsTotal);

  // Final price: total - discount + shipping
  return itemsTotal - discount + shipping;
}

module.exports = {
  calculateDiscount,
  calculateShipping,
  processOrder
};
```

**Benefits:**
- Descriptive function names
- Clear variable names
- JSDoc documentation
- Comments explaining business logic
- Easy to understand immediately

---

## Exercise: Add Context

Take this low-context code and improve it:

```javascript
function c(p, t) {
  let d = 0;
  if (t === 'p') d = p * 0.2;
  if (t === 'e') d = p * 0.4;
  return p - d;
}
```

**Your improvements:**
1. Rename function to be descriptive
2. Rename parameters with clear names
3. Add JSDoc documentation
4. Add comments explaining business logic
5. Use named constants where appropriate

**Solution (don't peek!):**

<details>
<summary>Click to see solution</summary>

```javascript
/**
 * Calculate final price after applying tier-based discounts
 * Business Rules:
 * - Premium tier: 20% discount
 * - Enterprise tier: 40% discount
 * - Standard tier: 0% discount
 *
 * @param {number} price - Base price in USD
 * @param {string} tier - User tier: 'standard', 'premium', or 'enterprise'
 * @returns {number} Final price after discount
 */
function calculateDiscountedPrice(price, tier) {
  const PREMIUM_DISCOUNT = 0.2;   // 20%
  const ENTERPRISE_DISCOUNT = 0.4; // 40%

  let discount = 0;

  // Premium users get 20% discount
  if (tier === 'premium') {
    discount = price * PREMIUM_DISCOUNT;
  }

  // Enterprise users get 40% discount
  if (tier === 'enterprise') {
    discount = price * ENTERPRISE_DISCOUNT;
  }

  return price - discount;
}
```

</details>

---

## Key Takeaways

**Good context includes:**
- ✅ Descriptive names (functions, variables, constants)
- ✅ JSDoc documentation
- ✅ Comments explaining "why" (business logic)
- ✅ Clear structure
- ✅ Named constants for magic numbers

**Avoid:**
- ❌ Cryptic abbreviations
- ❌ Single-letter variables (except loop counters)
- ❌ No documentation
- ❌ No comments
- ❌ Magic numbers without explanation
