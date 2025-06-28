# 🧪 Black Box API Challenge – Report

This report documents the behavior of each mysterious endpoint hosted at [https://blackbox-interface.vercel.app](https://blackbox-interface.vercel.app), as reverse-engineered by testing sample inputs and analyzing their outputs.

---

## ✅ 1. POST `/data`

- **Input:** `"racecar"`
- **Output:** `"InJhY2VjYXIi"`
- **Decoded Result:** `"racecar"`

### 📌 Inference:
Encodes the input string as **Base64**, including quotes.

---

## ✅ 2. GET `/time`

- **Output:** `{ "result": 8166848 }`

### 📌 Inference:
Returns a numerical **timestamp** or counter. Likely a custom time or internal tick count, not UTC or epoch time.

---

## ✅ 3. POST `/fizzbuzz`

- **Input:** `"racecar"`
- **Output:** `false`

### 📌 Inference:
Returns `true` or a string like "Fizz" or "Buzz" **only for numeric input** (e.g., 3 → Fizz, 5 → Buzz, 15 → FizzBuzz). Non-numeric input → `false`.

---

## ✅ 4. POST `/zap`

- **Input:** `"racecar"`
- **Output:** `"\"racecar\""` (i.e., `"racecar"` as a quoted string)

### 📌 Inference:
Echoes the input string with **quotes wrapped** (i.e., stringified JSON).

---

## ✅ 5. POST `/alpha`

- **Input:** `"racecar"`
- **Output:** `false`

### 📌 Inference:
Returns `true` **only if input contains only non-alphabet characters**. "racecar" has only letters → returns `false`.

---

## ✅ 6. POST `/glitch`

- **Input:** `"racecar"`
- **Output:** `"\"racecar\""` (i.e., JSON-quoted string)

### 📌 Inference:
Returns input with quotes. Possibly applies a transformation for certain patterns but unchanged for "racecar".

---
