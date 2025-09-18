# 🌐 REST API HTTP Status Cheat Sheet

Visual guide for backend and frontend teams: meanings, use cases, and handling.

---

## Status Table

| Status | Name | Meaning | Common Use Cases | Frontend Handling |
|--------|------|---------|-----------------|-----------------|
| **200** | OK | Successful request | Resource fetched/created/updated | Render data or empty state (`[]`) gracefully |
| **400** | Bad Request | Malformed or invalid request | Missing params, invalid JSON, wrong data type | Show validation errors. Don't crash. |
| **401** | Unauthorized | Not authenticated | Missing/invalid token, not logged in | Redirect to login or show "please log in." |
| **403** | Forbidden | Authenticated but no permission | Wrong role, ownership issues | Show "Access denied." |
| **404** | Not Found | Resource does not exist | Single resource missing | Show "Not found" or empty state. |
| **422** | Unprocessable Entity | Syntax correct but semantic errors | Validation or business-rule failures | Show field-specific errors/messages. |
| **500** | Internal Server Error | Server error or unexpected condition | DB failure, unhandled exceptions | Show generic error page. Retry/report. |

---

## 🌟 Color Code Guide

- **Green** → Success (200)  
- **Orange** → Client error (400–422)  
- **Red** → Server error (500+)  

---

## ✅ Quick Tips for Teams

1. **Collections vs Single Resources**
   - Collections → `200 []` if empty  
   - Single → `404` if missing

2. **Validation**
   - 400 → syntax/format errors  
   - 422 → semantic/business-rule validation

3. **Authentication & Authorization**
   - 401 → unauthenticated → login  
   - 403 → forbidden → access denied

4. **Frontend Handling**
   - Graceful handling per status → avoid console “red errors” for normal conditions

---

This cheat sheet ensures both **backend correctness** and **frontend user experience**, making cross-team API integration smooth and predictable.
