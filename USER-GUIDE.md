# Farm Manager - User Guide & Implementation Documentation

## Overview

Farm Manager is a web-based application designed specifically for small-to-medium scale farmers in Malawi. It helps you track your farming operations, understand profitability, and make better decisions for next season.

## Core Features

### 1. Dashboard
- **Quick Overview**: See your total revenue, costs, profit, and yield at a glance
- **Real-time Calculations**: Automatically calculates profit margins and performance metrics
- **Field Summary**: View all your fields and their performance in one place

### 2. Fields & Crops
- **Field Registration**: Add fields with name, size (in hectares), crop type, and location
- **Supported Crops**: Maize, Tobacco, Groundnuts, Soya, Cotton, and custom crops
- **Performance Tracking**: Each field shows costs, revenue, profit, and yield per hectare
- **Planting Date**: Track when each field was planted

### 3. Inputs & Costs
Track all your farming expenses:
- **Seeds**: Record seed purchases and quantities
- **Fertilizer**: Track basal and top dressing applications
- **Chemicals**: Log pesticides and herbicides
- **Labour**: Record planting, weeding, and harvest labour costs
- **Transport**: Track transport expenses
- **Equipment**: Log tool and equipment purchases
- **Other**: Any additional costs

### 4. Harvest & Yield
- **Harvest Recording**: Log harvest dates and quantities (in kg)
- **Quality Grading**: Track quality levels (Premium, Good, Fair, Poor)
- **Automatic Calculations**: System automatically calculates yield per hectare
- **Notes**: Add notes about moisture content, storage, etc.

### 5. Sales & Revenue
- **Sales Tracking**: Record when you sell your crops
- **Price Recording**: Track price per kg and total revenue
- **Buyer Information**: Note who you sold to (ADMARC, traders, exporters)
- **Payment Details**: Add notes about payment terms

### 6. Analytics & Insights
The system answers key questions:
- **Which crop is most profitable?** See profit by crop type
- **Which field performed best?** Compare profit per hectare across fields
- **Where did my money go?** Visual breakdown of costs by category
- **What was my profit margin?** Calculate (Revenue - Costs) / Revenue
- **Field Comparison Table**: Side-by-side comparison of all fields

### 7. Data Export
- **Full Data Backup**: Download all your data as JSON file
- **Data Ownership**: Your data stays on your device
- **Reset Option**: Clear all data if needed (with double confirmation)

## Getting Started

### First Time Setup

1. **Open the Application**
   - Open farm-manager.html in any web browser
   - Works offline once loaded
   - No internet required after first load

2. **Add Your First Field**
   - Click "Fields & Crops" in the sidebar
   - Click "Add New Field"
   - Enter:
     - Field name (e.g., "North Field", "Plot A")
     - Size in hectares (e.g., 2.5)
     - Crop type (select from dropdown)
     - Planting date (optional)
     - Location/notes (optional)
   - Click "Save Field"

3. **Record Your Costs**
   - Go to "Inputs & Costs"
   - Click "Record Input/Cost"
   - Select the date, field, and category
   - Enter description and amount in Malawi Kwacha (MK)
   - Click "Save Input"

4. **Record Harvest**
   - When you harvest, go to "Harvest & Yield"
   - Click "Record Harvest"
   - Enter date, field, quantity in kg, and quality
   - System automatically calculates yield per hectare

5. **Record Sales**
   - When you sell, go to "Sales & Revenue"
   - Click "Record Sale"
   - Enter quantity sold, price per kg, and buyer
   - System automatically calculates total revenue

## How to Use Throughout the Season

### At Planting Time
1. Add your fields with crop types and planting dates
2. Record seed costs
3. Record fertilizer purchases (basal dressing)
4. Record labour for land preparation and planting

### During Growing Season
1. Record fertilizer applications (top dressing)
2. Record chemical applications (pesticides, herbicides)
3. Record weeding labour
4. Track any additional costs

### At Harvest Time
1. Record harvest quantities for each field
2. Note quality grades
3. Record harvest labour costs
4. Track transport costs

### When Selling
1. Record each sale with date and quantity
2. Track price per kg
3. Note buyer information
4. Add payment terms in notes

### Season Review
1. Go to Analytics to see:
   - Which crops were most profitable
   - Which fields performed best
   - Where you spent the most money
   - Your overall profit margin
2. Export your data for backup
3. Use insights to plan next season

## Key Benefits

### Data-Driven Decisions
- **Know Your Numbers**: See exactly which crops and fields make money
- **Cost Awareness**: Understand where your money goes
- **Yield Tracking**: Monitor productivity per hectare
- **Price Intelligence**: Track what prices you received

### Practical Design
- **Simple Data Entry**: Quick forms with minimal typing
- **No Internet Needed**: Works completely offline
- **Local Storage**: All data saved on your device
- **Mobile Friendly**: Works on phones and tablets

### Farmer-Focused
- **Malawi Context**: All in Malawi Kwacha (MK)
- **Rain-fed Agriculture**: Designed for seasonal farming
- **Cash Crops**: Supports maize, tobacco, groundnuts, soya, cotton
- **Real Questions**: Answers what farmers actually need to know

## Tips for Best Results

### Accurate Record Keeping
- **Record costs immediately**: Don't wait - add expenses when they happen
- **Keep receipts**: Match your app data with physical receipts
- **Be detailed**: Add notes about quantities, suppliers, etc.
- **Separate fields**: Track each field individually for better insights

### Data Quality
- **Measure carefully**: Accurate field sizes = accurate yield calculations
- **Weigh harvests**: Use reliable scales for harvest weights
- **Record all costs**: Include small expenses - they add up
- **Note dates**: Helps understand timing and seasonal patterns

### Using Insights
- **Compare fields**: Learn which locations perform better
- **Analyze costs**: Identify where you can save money
- **Track trends**: See what worked year over year
- **Plan ahead**: Use data to make planting decisions

## Technical Information

### Data Storage
- All data stored in browser's localStorage
- Data persists between sessions
- Each device has its own data
- Export regularly for backup

### Offline Capability
- Application works completely offline
- No internet required after first load
- Offline indicator appears when disconnected
- All calculations happen on your device

### Data Privacy
- No data sent to servers
- Everything stays on your device
- You control your data
- Export and delete as needed

### Browser Compatibility
- Works on any modern browser
- Chrome, Firefox, Safari, Edge
- Works on mobile browsers
- Tested on Android and iOS

## Calculations Explained

### Field-Level Metrics
- **Total Costs**: Sum of all inputs for that field
- **Revenue**: Sum of all sales from that field
- **Profit**: Revenue minus Costs
- **Yield per Hectare**: Total harvest ÷ Field size

### Farm-Level Metrics
- **Total Revenue**: Sum of all sales across all fields
- **Total Costs**: Sum of all inputs across all fields
- **Net Profit**: Total Revenue - Total Costs
- **Profit Margin**: (Net Profit ÷ Total Revenue) × 100

### Analytics
- **Most Profitable Crop**: Crop type with highest total profit
- **Best Field**: Field with highest profit per hectare
- **Average Yield**: Total harvest ÷ Total farm area
- **Cost Breakdown**: Percentage of total costs by category

## Future Enhancements (Planned)

### Next Version
- Livestock module (cattle, goats, chickens)
- Multi-season comparison
- Weather tracking
- Loan/credit tracking
- Cooperative/group features

### Advanced Features
- PDF report generation
- SMS notifications
- Market price integration
- Satellite imagery integration
- Extension service integration

## Troubleshooting

### Data Not Saving
- Check browser settings allow localStorage
- Ensure you're not in private/incognito mode
- Try exporting data and refreshing page

### Can't See My Fields
- Make sure you saved the field properly
- Check you're on the right page
- Try refreshing the browser

### Numbers Don't Match
- Verify all costs are recorded
- Check field assignments are correct
- Ensure harvest weights are accurate
- Confirm sale quantities and prices

### Lost Data
- Export data regularly as backup
- Don't use browser's "Clear Data" function
- Don't uninstall browser without backup
- Keep export files in safe location

## Support & Feedback

This application is designed to grow with farmer feedback. Key areas for improvement:
- Ease of data entry
- Useful analytics
- Additional crop types
- Integration with other tools
- Language localization

## Getting Help

### Common Questions

**Q: How do I backup my data?**
A: Go to Export Data page and click "Download All Data (JSON)"

**Q: Can I use this on my phone?**
A: Yes! It works on any smartphone browser

**Q: What if I make a mistake?**
A: Currently you need to export, edit the JSON file, and re-import. Future versions will have edit/delete functions.

**Q: Can multiple people use this?**
A: It's designed for single farmer use. Each browser/device has separate data.

**Q: Does it work without internet?**
A: Yes! Once loaded, it works completely offline.

**Q: Can I share my data?**
A: Yes, export the JSON file and share it via WhatsApp, email, etc.

## Best Practices for Malawi Farmers

### Rainy Season (November - April)
1. Set up fields at start of season
2. Record all planting costs immediately
3. Track fertilizer applications with dates
4. Log weeding labour
5. Monitor costs weekly

### Harvest Time (April - June)
1. Weigh all harvests accurately
2. Record quality grades
3. Track harvest labour
4. Note storage costs
5. Document any losses

### Selling Season (May - September)
1. Record every sale
2. Track prices received
3. Note buyer details
4. Document transport costs
5. Keep payment records

### Off-Season (July - October)
1. Review analytics
2. Calculate total profit
3. Identify best crops/fields
4. Plan next season
5. Export data for safekeeping

## Customization Options

### Supported Crop Types
- Maize
- Tobacco
- Groundnuts
- Soya
- Cotton
- Other (for custom crops)

### Input Categories
- Seeds
- Fertilizer (Basal/Top Dressing)
- Chemicals (Pesticides/Herbicides)
- Labour (Planting/Weeding/Harvest)
- Transport
- Equipment/Tools
- Other

### Quality Grades
- Premium/Grade A
- Good/Grade B
- Fair/Grade C
- Poor/Reject

## Privacy & Security

### Your Data is Private
- No cloud storage
- No data transmission
- No user accounts
- No tracking

### Data Control
- You own all data
- Export anytime
- Delete anytime
- No lock-in

### Security Tips
- Keep device secure
- Export regularly
- Store backups safely
- Don't share device access

## Performance Tips

### Faster Data Entry
1. Use browser autofill for repeated buyers/suppliers
2. Enter data in batches (weekly is fine)
3. Keep a paper backup for field notes
4. Transfer to app when convenient

### Better Insights
1. Use consistent naming (e.g., all fields as "Field 1, 2, 3")
2. Record all costs, even small ones
3. Separate different crop cycles
4. Add notes for context

### Long-term Success
1. Export data after each season
2. Compare seasons year over year
3. Build historical database
4. Share learnings with other farmers

---

## Version Information
- Version: 1.0
- Release Date: February 2026
- Designed for: Malawian small-to-medium scale farmers
- Language: English (Chichewa version planned)
- Currency: Malawi Kwacha (MK)

## Credits
This application was designed with input from Malawian farming practices, focusing on:
- Rain-fed agriculture
- Cash crop farming
- Input cost sensitivity
- Seasonal variability
- Low digital literacy
- Offline-first design
- Data ownership
- Practical decision-making

---

**Remember**: This tool is only as good as the data you put in. Record everything, be accurate, and use the insights to make better farming decisions!
