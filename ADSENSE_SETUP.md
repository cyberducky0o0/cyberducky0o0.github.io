# Google AdSense Integration

This document outlines the comprehensive Google AdSense integration implemented across the website.

## AdSense Publisher ID
- **Publisher ID**: `ca-pub-4089158407852739`

## Ad Placements

### 1. Global Placements
- **Head Section** (`_includes/head.html`): Main AdSense script and Auto Ads
- **Footer** (`_includes/footer.html`): Banner ad before social links

### 2. Post Pages (`_layouts/post.html`)
- **Top Banner**: After post title and subtitle
- **In-Content**: After post content, before pagination
- **Sidebar**: In two-column layout (if enabled)

### 3. Home Page (`_layouts/home.html`)
- **Top Banner**: After hero section, before posts grid
- **Content Ad**: After posts grid, before pagination

### 4. Static Pages (`_layouts/page.html`)
- **Top Banner**: Before page content
- **Bottom Content**: After page content

### 5. Category Pages (`_layouts/category.html`)
- **Top Banner**: After category title
- **Content Ad**: After posts grid

### 6. Tags Page (`_layouts/tags.html`)
- **Top Banner**: Before tags list
- **Content Ad**: After all tag sections

## Ad Unit Types

### Banner Ads (`_includes/adsense-banner.html`)
- **Format**: Horizontal banner
- **Placement**: Top of pages, headers
- **Responsive**: Yes

### Content Ads (`_includes/adsense-content.html`)
- **Format**: In-article, fluid
- **Placement**: Within content areas
- **Features**: Advertisement label, bordered styling

### Sidebar Ads (`_includes/adsense-sidebar.html`)
- **Format**: Vertical rectangle
- **Placement**: Sidebar areas (two-column layouts)
- **Responsive**: Yes

### Mobile Ads (`_includes/adsense-mobile.html`)
- **Format**: Rectangle
- **Placement**: Mobile-optimized placements
- **Responsive**: Yes

### Auto Ads (`_includes/adsense-auto.html`)
- **Type**: Page-level ads
- **Placement**: Automatic by Google
- **Features**: AI-optimized placement

## Styling

Custom CSS styles are defined in `_sass/_adsense.scss` and include:
- Responsive design for different screen sizes
- Proper spacing and margins
- Advertisement labels
- Mobile optimizations
- Hide certain ads on very small screens

## Ad Slot IDs

**Note**: The current implementation uses placeholder ad slot IDs. You need to:

1. **Create actual ad units** in your Google AdSense account
2. **Replace placeholder slot IDs** with real ones:
   - Banner ads: `1234567890` → Your banner slot ID
   - Sidebar ads: `9876543210` → Your sidebar slot ID
   - Content ads: `5555555555` → Your content slot ID
   - Mobile ads: `1111111111` → Your mobile slot ID

## Setup Instructions

1. **Verify Publisher ID**: Ensure `ca-pub-4089158407852739` is your correct publisher ID
2. **Create Ad Units**: In AdSense dashboard, create ad units for each placement type
3. **Update Slot IDs**: Replace placeholder IDs with actual slot IDs from AdSense
4. **Test Implementation**: Use AdSense preview tools to verify ad display
5. **Monitor Performance**: Check AdSense reports for ad performance

## Files Modified

- `_includes/head.html` - Main AdSense script
- `_includes/footer.html` - Footer ad placement
- `_layouts/post.html` - Post page ads
- `_layouts/home.html` - Home page ads
- `_layouts/page.html` - Static page ads
- `_layouts/category.html` - Category page ads
- `_layouts/tags.html` - Tags page ads
- `_sass/main.scss` - Include AdSense styles
- `_sass/_adsense.scss` - AdSense-specific styles

## Files Created

- `_includes/adsense.html` - Generic ad unit
- `_includes/adsense-banner.html` - Banner ad unit
- `_includes/adsense-sidebar.html` - Sidebar ad unit
- `_includes/adsense-content.html` - Content ad unit
- `_includes/adsense-mobile.html` - Mobile ad unit
- `_includes/adsense-auto.html` - Auto ads script

## Best Practices

1. **Ad Density**: Current implementation provides good ad coverage without overwhelming users
2. **User Experience**: Ads are styled to integrate well with site design
3. **Mobile Optimization**: Responsive design ensures good mobile experience
4. **Performance**: Async loading prevents ads from blocking page rendering
5. **Compliance**: Implementation follows AdSense policies and guidelines

## Next Steps

1. Replace placeholder ad slot IDs with real ones from your AdSense account
2. Test all ad placements across different devices and screen sizes
3. Monitor ad performance and adjust placements as needed
4. Consider A/B testing different ad formats and positions
5. Ensure compliance with privacy policies and GDPR requirements
