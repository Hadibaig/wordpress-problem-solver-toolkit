# Case 01 — Custom Login Redirect Using Hooks

**Category:** Hooks, Actions & Filters  
**Platform:** WordPress  
**Difficulty:** Intermediate  
**Time to Implement:** 15 minutes  
**Status:** ✅ Implemented

---

## ❗ Requirement

Client wanted:
- Admin users → wp-admin
- Customers → My Account page
- Subscribers → homepage

---

## 🔍 Solution Approach

Used WordPress login hook:

```php
add_filter('login_redirect', 'custom_login_redirect', 10, 3);

function custom_login_redirect($redirect_to, $request, $user) {
    
    if (isset($user->roles) && is_array($user->roles)) {

        if (in_array('administrator', $user->roles)) {
            return admin_url();
        }

        if (in_array('customer', $user->roles)) {
            return site_url('/my-account');
        }

        return site_url('/');
    }

    return $redirect_to;
}
```

---

## 🎯 Result

- Role-based login redirect implemented
- Improved UX for different user types

---

## 💡 Lesson

Hooks allow modifying WordPress behavior without touching core files.


- *By [Mirza Hadi](https://hadi-mirza.com) —
Full-Stack Developer & Technical Problem Solver*  
*📰 [DCXherald Newsletter](https://linkedin.com/in/hadibaig)*
