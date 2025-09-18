# EbilPaul's Guide For Api Integration For Dumb Frontend Devs
This is a repository with clear guidelines for frontend devs to gracefully and clearly handle backend request status codes especially 404's


## Why I Made This Guide

A while back, I was working on a project with a friend, integrating the backend APIs with their frontend. Everything was going smoothly until the frontend started throwing errors every time a request returned a `404` Not Found.

From a backend perspective, `404` is perfectly acceptable, it means “this resource doesn’t exist,” which is exactly what REST semantics dictate. Collections should return `200 []` if empty, and single resources return `404` if missing. But many frontend request libraries, like Axios, immediately throw an error on `404`, treating it like a fatal crash.

To get the project moving, I had to bend the rules: instead of returning `404` for some endpoints, I returned empty lists (`[]`). This “solved” the frontend crashes, but I knew it wasn’t semantically correct, it blurred the line between “resource does not exist” and “resource exists but is empty.”

That experience made me realize there’s a real gap in understanding between backend and frontend teams:

* Backend should return proper HTTP status codes for correctness.

* Frontend should gracefully handle `404`, `400`, `422`, and other status codes without panicking.

This cheat sheet is my attempt to bridge that gap. It clearly explains what each status code means, how to handle it on the frontend, and best practices for both sides. By following this, teams can avoid hacks like replacing `404` with `[]` while still keeping user experiences smooth.

## 🌐 REST API HTTP Status Cheat Sheet

Visual guide for backend and frontend teams: meanings, use cases, and handling.

---

### Status Table

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

### 🌟 Color Code Guide

- **Green** → Success (200)  
- **Orange** → Client error (400–422)  
- **Red** → Server error (500+)  

---

### ✅ Quick Tips for Teams

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
