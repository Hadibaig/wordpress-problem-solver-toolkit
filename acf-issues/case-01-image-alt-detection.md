# Case 02 — ACF Image ALT Text Not Showing on Frontend

**Category:** ACF Issues  
**Platform:** WordPress (ACF + Custom Theme)  
**Difficulty:** Intermediate  
**Time to Diagnose:** 30–40 minutes  
**Status:** ✅ Resolved

---

## ❗ The Symptom

Client reported that images managed via Advanced Custom Fields (ACF):

- Displayed correctly on frontend
- But ALT attributes were missing or empty
- SEO tools flagged "Missing image ALT text"

Even though ALT text was already set in the WordPress media library.

---

## 🔍 Diagnosis Steps

### Step 1 — Checked ACF image field output

Found template using:

```php
<?php $image = get_field('your_image_field'); ?>
<img src="<?php echo $image; ?>" alt="">
```

This immediately showed the issue:
- No ALT being passed
- Only raw image URL used

---

### Step 2 — Checked ACF return format

ACF image field was set to:

- ❌ Image URL (most common mistake)

This means:
- Only URL is returned
- No ALT, ID, or metadata available

---

### Step 3 — Confirmed root limitation

ACF image fields support 3 return formats:

- Image Array → full metadata (URL, ALT, sizes, etc.)
- Image URL → only string URL
- Image ID → attachment ID only

The issue came from using **Image URL**, which removes access to ALT text completely.

---

## 🎯 Root Cause

ACF image field was configured to return **URL only**, and template code was not explicitly fetching ALT text separately.

As a result:
- ALT attribute remained empty
- Even though media library contained valid ALT text

---

## ✅ The Fix

### Fix 1 — Use Image Array (Recommended)

Updated ACF field:
- Return Format → **Image Array**

Updated template:

```php
<?php 
$image = get_field('your_image_field');

if( $image ): ?>
    <img 
        src="<?php echo esc_url($image['url']); ?>" 
        alt="<?php echo esc_attr($image['alt']); ?>"
        width="<?php echo esc_attr($image['width']); ?>"
        height="<?php echo esc_attr($image['height']); ?>"
    >
<?php endif; ?>
```

---

### Fix 2 — If using Image ID (Best Practice)

```php
<?php 
$image_id = get_field('your_image_field');

if( $image_id ):
    echo wp_get_attachment_image($image_id, 'full');
endif;
?>
```

✔ Automatically handles:
- ALT text  
- Responsive images  
- Width/height  
- srcset  

---

### Fix 3 — If stuck with Image URL

```php
<?php 
$image_url = get_field('your_image_field');

if( $image_url ):
    $image_id  = attachment_url_to_postid($image_url);
    $image_alt = get_post_meta($image_id, '_wp_attachment_image_alt', true);
?>
    <img 
        src="<?php echo esc_url($image_url); ?>" 
        alt="<?php echo esc_attr($image_alt); ?>"
    >
<?php endif; ?>
```

---

## ⚠️ Important Observation

ALT text in WordPress comes from:

- Media Library attachment metadata
NOT directly from ACF field itself.

ACF only exposes it when return format supports metadata.

---

## 🧠 Root Insight

Most developers break ALT text in ACF because:

- They choose **Image URL return format for simplicity**
- Then forget that metadata is lost
- And hardcode empty ALT attributes

---

## 💡 Best Practice (Production Standard)

For all ACF image fields:

✔ Use **Image ID return format**  
✔ Render with `wp_get_attachment_image()`  
✔ Set ALT text in Media Library only  

Example:

```php
<?php 
$image_id = get_field('your_image_field');
if( $image_id ) echo wp_get_attachment_image($image_id, 'large');
?>
```

---

## 📌 Final Lesson

ACF does not break SEO — incorrect implementation does.

Understanding return formats is critical:

- URL → visual only, no metadata  
- Array → full control  
- ID → WordPress-managed output (recommended)

A proper setup ensures:
- No missing ALT attributes
- Better accessibility
- SEO compliance
- Cleaner templates

---

*By [Mirza Hadi](https://hadi-mirza.com) —
Full-Stack Developer & Technical Problem Solver*  
*📰 [DCXherald Newsletter](https://linkedin.com/in/hadibaig)*
