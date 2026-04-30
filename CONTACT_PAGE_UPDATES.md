# Contact Page Layout Redesign - Documentation

## Overview
The contact page (page ID 124) underwent a comprehensive layout redesign to improve visual hierarchy, spacing, and user experience. The main changes focused on responsive flexbox layout, icon sizing, map image scaling, and button positioning.

## Files Modified
- **[contact/index.html](contact/index.html)** - Main contact page with embedded CSS styling
- **[wp-json/wp/v2/pages/124.json](wp-json/wp/v2/pages/124.json)** - REST API endpoint with complete page content

## Layout Structure

### Three-Column Grid
The contact page uses a three-column flex layout with equal distribution:
- **Column 1 (pgc-124-0-0)**: Contact icons/information (Teléfono, Celular, Correo Electrónico)
- **Column 2 (pgc-124-0-1)**: Contact form ("Envíenos un mensaje")
- **Column 3 (pgc-124-0-2)**: Map section ("Donde estamos?")

### Key CSS Classes
- `#pl-124` - Main panel layout container
- `#pg-124-0` - Grid row wrapper
- `#pgc-124-0-0/1/2` - Grid cells (columns)
- `.tg-service-widget` - Contact item widget
- `.map-open-link` - Google Maps link wrapper

## CSS Styling Implementation

### Core Layout
```css
#pl-124 #pg-124-0 {
  display: flex;
  flex-wrap: wrap;
  align-items: flex-start;
  gap: 20px;
}
```
- **Flexbox** layout for responsive design
- **flex-start** alignment keeps columns at top
- **20px gap** for spacing between columns

### Contact Icons Column (Column 1)
```css
#pl-124 #pgc-124-0-0 {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  max-width: 140px;
  flex-shrink: 0;
}
```
- **max-width: 140px** - Fixed narrow width prevents overflow
- **flex-shrink: 0** - Prevents column from shrinking
- **flex-direction: column** - Stacks items vertically

### Service Widgets (Contact Items)
```css
#pl-124 .tg-service-widget.tg-service-layout-2 {
  margin: 0;
  padding: 8px 0;
}

#pl-124 .tg-service-widget {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

#pl-124 .tg-service-widget .service-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
}
```
- **Centered alignment** for icons and text
- **8px padding** for tight spacing
- **No margins** for compact layout

### Icon Sizing
```css
#pl-124 .tg-service-widget .service-icon-wrap {
  width: 60px;
  height: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 6px;
}
```
- **60x60px circle** for each icon
- **6px margin-bottom** between icon and text

### Text Sizing
```css
#pl-124 .tg-service-widget .service-title-wrap {
  margin: 0;
  font-size: 12px;
  font-weight: 600;
}

#pl-124 .tg-service-widget .service-content-wrap {
  margin: 0;
  font-size: 11px;
  margin-top: 4px;
}
```
- **12px title**, **11px content** - Compact sizing
- **4px spacing** between title and content

### Map Image & Button
```css
#pl-124 .map-open-link img {
  height: auto;
  width: 90%;
  display: block;
  border: none;
  margin: 0 auto;
}

#pl-124 .map-open-link {
  display: block;
  margin: 0;
  padding: 0;
}

#panel-124-0-2-1 {
  display: flex;
  flex-direction: column;
}

#panel-124-0-2-1 > p {
  margin: 0;
}

#panel-124-0-2-1 > p:first-of-type {
  flex: 1;
}

#panel-124-0-2-1 > p:last-child {
  margin: 0;
}

#panel-124-0-2-1 > p:last-child a {
  display: block;
  width: fit-content;
}
```
- **90% width** - Reduces image size by 10%
- **0 margin/padding** - Removes all gaps between image and button
- **flex: 1** on first paragraph - Pushes button down to bottom
- Button sits directly below image with no spacing

### Responsive Design (Mobile)
```css
@media (max-width: 980px) {
  #pl-124 #pg-124-0 {
    display: block;
    gap: 0;
  }
  
  #pl-124 #pgc-124-0-0,
  #pl-124 #pgc-124-0-1,
  #pl-124 #pgc-124-0-2 {
    display: block;
  }
  
  #pl-124 .map-open-link img {
    width: 100%;
  }
}
```
- Converts flex layout to block stacking
- Image expands to full width on mobile
- Single column layout

## Visual Hierarchy

### Before Changes
- Yellow overlay on map image (removed)
- Inconsistent column heights
- Large spacing between elements
- Contact info not visible without scrolling

### After Changes
1. **Contact Icons Column** - Compact, left-aligned, ~140px width
2. **Contact Form** - Full flex, centered
3. **Map Section** - Full flex, map fills space, button touches image
4. All columns align at top (`align-items: flex-start`)
5. Email contact info now visible without scrolling

## Interactive Elements

### Contact Info Items
- Icon (60x60px circle with FontAwesome)
- Title (bold, 12px)
- Content (11px, can include phone numbers or email)

### Contact Form
- Standard HTML form
- Hosted content (likely from contact-form-7 plugin)
- Submit button ("Enviar")

### Map Section
- Static Google Maps image (550x640px)
- Clickable to open interactive map
- Yellow button ("ABRIR EN GOOGLE MAPS") positioned directly below
- No padding between image and button

## Data Structure (JSON)

The page content is stored in two locations:

1. **HTML File** - Primary source
   ```
   contact/index.html → <style>...</style> + page markup
   ```

2. **JSON API** - REST endpoint
   ```
   wp-json/wp/v2/pages/124.json → content.rendered (same styling + markup)
   ```

Both files must be kept in sync. The HTML is the source of truth; JSON is updated via Python scripts.

## Maintenance Notes

### Updating the Layout
1. Edit CSS in `<style>` block in [contact/index.html](contact/index.html)
2. Update [wp-json/wp/v2/pages/124.json](wp-json/wp/v2/pages/124.json) with matching CSS
3. Use Python script to sync JSON if making bulk changes
4. Test responsive layout on mobile (980px breakpoint)

### Adding New Contact Method
To add a fourth contact item:
1. Add new `.tg-service-widget` block in Column 1
2. Include `.service-icon-wrap`, `.service-title-wrap`, and `.service-content-wrap`
3. Adjust `max-width` if needed for Column 1
4. CSS will automatically style new widget

### Adjusting Spacing
- **Icon size**: Change `width/height` in `.service-icon-wrap` (currently 60px)
- **Gap between columns**: Change `gap` property in `#pg-124-0` (currently 20px)
- **Map size**: Adjust `.map-open-link img` width percentage (currently 90%)
- **Button position**: Remove `margin: 0` on `.map-open-link` if spacing needed

## Browser Compatibility
- Modern flexbox support required (IE 11+ with prefixes)
- CSS Grid not used (better mobile support)
- FontAwesome 4.x icons (fa-phone, fa-mobile, fa-envelope-o)

## Performance Considerations
- No JavaScript animations
- Single CSS file embedded in page
- Google Maps embedded as static image (reduces load)
- 90% width map image reduces bandwidth

## Related JSON Files
- [wp-json/wp/v2/pages/124.json](wp-json/wp/v2/pages/124.json) - Contact page (this page)
- [wp-json/wp/v2/pages/137.json](wp-json/wp/v2/pages/137.json) - About page
- [wp-json/wp/v2/pages/221.json](wp-json/wp/v2/pages/221.json) - Homepage

---
**Last Updated**: April 30, 2026  
**Status**: ✅ Final layout deployed
