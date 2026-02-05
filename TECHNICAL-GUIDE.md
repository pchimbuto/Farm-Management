# Farm Manager - Technical Implementation Guide

## Architecture Overview

### Technology Stack
- **Frontend**: Pure HTML5, CSS3, JavaScript (ES6+)
- **Storage**: Browser localStorage API
- **Framework**: Vanilla JS (no dependencies)
- **Design**: Custom CSS with CSS Variables
- **Offline**: Service Worker ready (not yet implemented)

### Design Philosophy
1. **Zero Dependencies**: No frameworks, no build process, no npm
2. **Offline First**: Works completely without internet
3. **Progressive Enhancement**: Degrades gracefully
4. **Mobile First**: Responsive design from ground up
5. **Data Ownership**: User controls all data
6. **Low Bandwidth**: Single HTML file, minimal assets
7. **Accessibility**: Semantic HTML, keyboard navigation

## Data Model

### Core Entities

```javascript
farmData = {
  version: '1.0',          // Schema version
  fields: [],              // Array of field objects
  inputs: [],              // Array of input/cost records
  harvests: [],            // Array of harvest records
  sales: []                // Array of sale records
}
```

### Field Schema
```javascript
field = {
  id: timestamp,           // Unique identifier
  name: string,            // Field name
  size: number,            // Size in hectares
  crop: string,            // Crop type
  plantingDate: string,    // ISO date string
  location: string,        // Description/notes
  createdAt: string        // ISO timestamp
}
```

### Input Schema
```javascript
input = {
  id: timestamp,           // Unique identifier
  date: string,            // ISO date string
  fieldIndex: number,      // Index in fields array
  category: string,        // Input category
  description: string,     // Item description
  quantity: string,        // Quantity/unit
  cost: number,            // Cost in MK
  createdAt: string        // ISO timestamp
}
```

### Harvest Schema
```javascript
harvest = {
  id: timestamp,           // Unique identifier
  date: string,            // ISO date string
  fieldIndex: number,      // Index in fields array
  quantity: number,        // Weight in kg
  quality: string,         // Quality grade
  notes: string,           // Additional notes
  createdAt: string        // ISO timestamp
}
```

### Sale Schema
```javascript
sale = {
  id: timestamp,           // Unique identifier
  date: string,            // ISO date string
  fieldIndex: number,      // Index in fields array
  quantity: number,        // Weight in kg
  pricePerKg: number,      // Price per kg in MK
  total: number,           // Total amount (calculated)
  buyer: string,           // Buyer name
  notes: string,           // Additional notes
  createdAt: string        // ISO timestamp
}
```

## Storage Implementation

### localStorage Usage
```javascript
// Key: 'farmManagerData'
// Value: JSON stringified farmData object

// Load
const farmData = JSON.parse(localStorage.getItem('farmManagerData'));

// Save
localStorage.setItem('farmManagerData', JSON.stringify(farmData));

// Clear
localStorage.removeItem('farmManagerData');
```

### Storage Limits
- localStorage typically has 5-10MB limit
- Current schema: ~1KB per 10 records
- Estimated capacity: 50,000+ records before issues
- Recommend export after 5000+ records

### Data Persistence
- Persists across browser sessions
- Survives page refresh
- Cleared when browser cache cleared
- Not shared across devices/browsers

## Key Functions

### Initialization
```javascript
function initApp() {
  loadData();              // Load from localStorage
  setupNavigation();       // Bind navigation events
  updateDashboard();       // Calculate and display stats
  renderFields();          // Display field cards
  renderInputs();          // Display inputs table
  renderHarvests();        // Display harvests table
  renderSales();           // Display sales table
  updateAnalytics();       // Calculate analytics
  checkOnlineStatus();     // Setup offline indicator
}
```

### Calculations

#### Field-Level Calculations
```javascript
// Total costs for a field
function calculateFieldCosts(fieldIndex) {
  return farmData.inputs
    .filter(i => i.fieldIndex === fieldIndex)
    .reduce((sum, i) => sum + i.cost, 0);
}

// Total revenue for a field
function calculateFieldRevenue(fieldIndex) {
  return farmData.sales
    .filter(s => s.fieldIndex === fieldIndex)
    .reduce((sum, s) => sum + s.total, 0);
}

// Total yield for a field
function calculateFieldYield(fieldIndex) {
  return farmData.harvests
    .filter(h => h.fieldIndex === fieldIndex)
    .reduce((sum, h) => sum + h.quantity, 0);
}
```

#### Farm-Level Calculations
```javascript
// Total costs across farm
function calculateTotalCosts() {
  return farmData.inputs.reduce((sum, i) => sum + i.cost, 0);
}

// Total revenue across farm
function calculateTotalRevenue() {
  return farmData.sales.reduce((sum, s) => sum + s.total, 0);
}

// Total yield across farm
function calculateTotalYield() {
  return farmData.harvests.reduce((sum, h) => sum + h.quantity, 0);
}
```

## UI Components

### Modal System
```javascript
// Show modal
function openModal(modalId) {
  document.getElementById(modalId).classList.add('active');
}

// Hide modal
function closeModal(modalId) {
  document.getElementById(modalId).classList.remove('active');
}

// Modal structure
<div class="modal">
  <div class="modal-content">
    <div class="modal-header">...</div>
    <div class="modal-body">...</div>
    <div class="modal-footer">...</div>
  </div>
</div>
```

### Page Navigation
```javascript
// Single page application approach
function showPage(pageName) {
  // Hide all pages
  document.querySelectorAll('.page').forEach(page => 
    page.classList.add('hidden')
  );
  
  // Show selected page
  document.getElementById(`page-${pageName}`)
    .classList.remove('hidden');
  
  // Update page-specific data
  if (pageName === 'analytics') updateAnalytics();
}
```

### Dynamic Rendering
```javascript
// Pattern for rendering lists
function renderItems() {
  const container = document.getElementById('container');
  
  if (items.length === 0) {
    container.innerHTML = emptyStateHTML;
    return;
  }
  
  let html = items.map(item => `
    <div class="item">
      ${item.name}
    </div>
  `).join('');
  
  container.innerHTML = html;
}
```

## Responsive Design

### Breakpoints
```css
/* Mobile-first approach */

/* Base styles: Mobile (0-767px) */

/* Tablet (768px+) */
@media (min-width: 768px) {
  /* Tablet-specific styles */
}

/* Desktop (1024px+) */
@media (min-width: 1024px) {
  /* Desktop-specific styles */
}
```

### Mobile Considerations
- Touch-friendly targets (48px minimum)
- Simplified navigation on small screens
- Collapsible sidebar
- Single column layouts
- Reduced padding/margins
- Larger form inputs

## Performance Optimization

### Rendering Strategy
1. **Lazy Rendering**: Only render visible page
2. **Batch Updates**: Update DOM once per change set
3. **Event Delegation**: Use bubbling for dynamic content
4. **Minimal Reflows**: Use CSS transforms over position changes

### Storage Optimization
1. **Selective Loading**: Load only needed data
2. **Index by ID**: Use timestamps for O(1) lookup
3. **Avoid Deep Copies**: Reference when possible
4. **Debounce Saves**: Wait for input completion

### Memory Management
1. **Clear Event Listeners**: Remove when not needed
2. **Avoid Global Scope**: Use IIFE or modules
3. **Garbage Collection**: Null large objects
4. **Limit DOM Nodes**: Virtualize long lists (future)

## Extensibility

### Adding New Crop Types
```javascript
// In field modal
<select name="cropType">
  <option value="Maize">Maize</option>
  <option value="NewCrop">New Crop Name</option>
</select>
```

### Adding New Input Categories
```javascript
// In input modal
<select name="inputCategory">
  <option value="Seeds">Seeds</option>
  <option value="NewCategory">New Category</option>
</select>
```

### Schema Migration
```javascript
function migrateData(oldData, oldVersion) {
  if (oldVersion === '1.0' && currentVersion === '1.1') {
    // Add new fields with defaults
    oldData.fields.forEach(field => {
      field.newProperty = defaultValue;
    });
    oldData.version = '1.1';
  }
  return oldData;
}
```

## Future Enhancements

### Phase 1 (Next 3 months)
- [ ] Edit/delete functionality
- [ ] Multiple seasons support
- [ ] Basic charts (Chart.js integration)
- [ ] CSV export option
- [ ] Print-friendly reports

### Phase 2 (6 months)
- [ ] Livestock module
- [ ] Weather tracking
- [ ] Loan/credit tracking
- [ ] Photo attachments
- [ ] Chichewa language support

### Phase 3 (12 months)
- [ ] Service Worker for true PWA
- [ ] IndexedDB for larger datasets
- [ ] SMS notifications
- [ ] Market price integration
- [ ] Multi-user (cooperative) features
- [ ] Cloud backup option

## Testing Strategy

### Manual Testing Checklist
- [ ] Add field
- [ ] Add input with costs
- [ ] Add harvest with yield
- [ ] Add sale with revenue
- [ ] Verify dashboard calculations
- [ ] Check analytics insights
- [ ] Test export functionality
- [ ] Verify offline functionality
- [ ] Test responsive design
- [ ] Check data persistence

### Browser Compatibility
- Chrome/Edge: Full support
- Firefox: Full support
- Safari: Full support (iOS 12+)
- Opera: Full support
- Internet Explorer: Not supported

### Device Testing
- Android phones (Chrome)
- iPhones (Safari)
- Tablets (Android/iOS)
- Desktop browsers
- Low-end devices (512MB RAM)

## Security Considerations

### Data Privacy
- No external API calls
- No analytics/tracking
- No third-party scripts
- No cookies
- localStorage only

### Input Validation
```javascript
// Server-side validation not needed (no server)
// Client-side validation:

// Required fields
<input required>

// Number validation
<input type="number" step="0.01" min="0">

// Date validation
<input type="date">

// JavaScript validation
if (!value || value <= 0) {
  alert('Please enter a valid amount');
  return;
}
```

### XSS Prevention
```javascript
// Use textContent, not innerHTML for user data
element.textContent = userInput;

// If HTML needed, sanitize:
function sanitize(str) {
  const div = document.createElement('div');
  div.textContent = str;
  return div.innerHTML;
}
```

## Deployment

### Static Hosting Options
1. **File System**: Double-click HTML file
2. **GitHub Pages**: Free, version controlled
3. **Netlify**: Free, custom domain
4. **Vercel**: Free, automatic deployments
5. **AWS S3**: Pay per use
6. **Google Drive**: Share HTML file
7. **USB Drive**: Portable, offline

### No Build Process Needed
- Single HTML file
- No compilation
- No bundling
- No dependencies
- Copy and deploy

### Updates
1. Download new version
2. Export data from old version
3. Open new version
4. Data automatically migrates (if schema compatible)
5. Or manually import exported data

## Localization (Future)

### Chichewa Support
```javascript
const translations = {
  en: {
    dashboard: 'Dashboard',
    fields: 'Fields & Crops',
    // ... more
  },
  ny: {  // Chichewa
    dashboard: 'Chombocho',
    fields: 'Minda ndi Mbewu',
    // ... more
  }
};

function t(key) {
  const lang = localStorage.getItem('language') || 'en';
  return translations[lang][key] || key;
}
```

### Number Formatting
```javascript
// Already locale-aware
new Intl.NumberFormat('en-MW').format(amount);

// Currency
new Intl.NumberFormat('en-MW', {
  style: 'currency',
  currency: 'MWK'
}).format(amount);
```

## Analytics & Insights

### Current Calculations

1. **Most Profitable Crop**
   - Group sales by crop type
   - Subtract costs by crop type
   - Rank by profit

2. **Best Performing Field**
   - Calculate profit per hectare
   - Rank fields by profitability

3. **Cost Breakdown**
   - Group inputs by category
   - Calculate percentage of total
   - Visual bar chart representation

4. **Profit Margin**
   - (Revenue - Costs) / Revenue × 100

5. **Average Yield**
   - Total harvest / Total area

### Advanced Analytics (Future)
- Trend analysis across seasons
- Cost per kg produced
- ROI by input type
- Optimal planting windows
- Yield prediction models

## API Integration (Future)

### Weather Data
```javascript
// Potential integration with weather APIs
async function getWeather(latitude, longitude) {
  // Local weather service API
  // Store historical data
  // Correlate with yields
}
```

### Market Prices
```javascript
// Potential integration with ADMARC/market data
async function getMarketPrices(crop) {
  // Fetch current prices
  // Compare to user's sales
  // Alert on good selling opportunities
}
```

## Contributing

### Code Style
- 2-space indentation
- camelCase for variables
- Clear function names
- Comments for complex logic
- Semantic HTML
- BEM-like CSS naming

### Pull Request Process
1. Fork repository
2. Create feature branch
3. Test thoroughly
4. Update documentation
5. Submit PR with description

### Reporting Issues
1. Describe expected behavior
2. Describe actual behavior
3. Steps to reproduce
4. Browser/device info
5. Screenshots if relevant

## License & Credits

### Open Source License
- MIT License (suggested)
- Free to use, modify, distribute
- Attribution appreciated

### Technology Credits
- Google Fonts (Lexend, DM Mono)
- Modern browser APIs
- CSS Grid and Flexbox
- localStorage API

---

## Developer Notes

### Why Vanilla JS?
1. **Zero dependencies** = No supply chain attacks
2. **Always works** = No framework deprecation
3. **Lightweight** = Fast on low-end devices
4. **Educational** = Easy to understand and modify
5. **Portable** = Works anywhere HTML works

### Why localStorage?
1. **Simple** = Easy mental model
2. **Synchronous** = No async complexity
3. **Universal** = All browsers support
4. **Offline** = No server needed
5. **Private** = Data never leaves device

### Design Decisions

**Single HTML File**
- Easier distribution (WhatsApp, email, USB)
- No broken links
- Truly portable
- Self-contained

**No Backend**
- Reduced complexity
- No hosting costs
- Better privacy
- Faster development
- Easier maintenance

**Malawi Focus**
- MK currency
- Local crops (maize, tobacco, groundnuts)
- Rain-fed agriculture context
- Low connectivity assumption
- Mobile-first (most users on phones)

### Limitations

**Current Limitations**
- Single user only
- No cloud sync
- No real-time collaboration
- Limited to 5MB data
- No automatic backups
- No edit/delete (yet)

**By Design**
- Simple is better than complex
- Offline is better than online
- Privacy is better than convenience
- Ownership is better than rental

---

**Version**: 1.0  
**Last Updated**: February 2026  
**Maintainer**: Open source community  
**Status**: Production ready
