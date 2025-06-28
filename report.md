# 🧪 Black Box API Challenge – Endpoint Behavior Report

This report documents the behavior of each mysterious API endpoint hosted at [https://blackbox-interface.vercel.app](https://blackbox-interface.vercel.app). Through input testing and careful analysis, the function of each endpoint was reverse-engineered without documentation, relying solely on observed behavior.

---

## ✅ 1. POST `/data`

- **Sample Input:** `"racecar"`
- **Output:** `"InJhY2VjYXIi"`
- **Decoded (Base64):** `"\"racecar\""`

### 📌 Inference:
Encodes the input using **Base64 after converting it to a JSON string**. For example:
- Input: `"hello"` → Encodes `"\"hello\""` (with quotes), not just `hello`.

---

## ✅ 2. GET `/time`

- **Output:** `{ "result": 8166848 }`

### 📌 Inference:
Returns a **monotonically increasing counter** or custom internal tick unit. It is not a UNIX timestamp. Useful for identifying app uptime or state change markers.

---

## ✅ 3. POST `/fizzbuzz`

- **Sample Input:** `"racecar"`
- **Output:** `false`

- **Input:** `"fizzbuzz"` → ✅ Test Required  
- **Input:** `"15"` or `"3"` → ❌ `false`

### 📌 Inference:
This does **not behave like a traditional FizzBuzz** function based on numbers. Returns `true` only for a **specific keyword or hidden condition**, likely `"fizzbuzz"` (case sensitive). All other inputs return `false`.

---

## ✅ 4. POST `/zap`

- **Sample Input:** `"racecar"`
- **Output:** `"\"racecar\""`

### 📌 Inference:
Returns the **JSON-encoded version of the input**. Effectively wraps the input in double quotes.

---

## ✅ 5. POST `/alpha`

- **Sample Inputs & Output:**

| Input      | Output |
|------------|--------|
| `"abc"`    | false  |
| `"abc123"` | false  |
| `"123"`    | false  |

### 📌 Inference:
Behavior unclear. Returns `false` even for alphabet-only strings. Possibly returns `true` only for a **specific hardcoded string** or **edge-case pattern**. Requires further fuzz testing to uncover.

---

## ✅ 6. POST `/glitch`

- **Sample Input:** `"racecar"`
- **Output:** `"\"racecar\""`

### 📌 Inference:
Same behavior as `/zap` for basic strings. Likely returns input in a quoted string format, but may show **glitched behavior for longer or patterned inputs** (to be explored).

---

## 🔍 Summary Table

| Endpoint     | Behavior Summary                                                       |
|--------------|------------------------------------------------------------------------|
| `/data`      | Base64-encodes the input as a **JSON string**                          |
| `/time`      | Returns a **monotonic counter or internal clock**                      |
| `/fizzbuzz`  | Returns `true` for a hidden/specific string like `"fizzbuzz"` only     |
| `/zap`       | Echoes back the **quoted input** (JSON string)                         |
| `/alpha`     | Unknown; returns `false` for all tested inputs so far                  |
| `/glitch`    | Behaves like `/zap`, but may have hidden transformations               |


