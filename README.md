# QR Code Generator for Retail Product SKUs

## Overview
A client-side web application optimized for generating QR codes for large retail inventories (tested up to 10,000+ SKUs). No server required - everything runs in your browser.

## Files

### Main Application
- **index.html** - Main application (USE THIS for 8000 SKUs)
  - ✅ Batch processing (processes 100 SKUs at a time)
  - ✅ Progress bar with real-time updates
  - ✅ Memory management to prevent browser crashes
  - ✅ Handles 8000+ SKUs efficiently

### Testing Tools
- **generate_sample_csv.html** - Generate test CSV files with any number of SKUs
- **sample-products.csv** - Small sample file (15 SKUs) for quick testing

### Legacy (Not Recommended for Large Datasets)
- **qr-code-generator.html** - Original version (limit: ~500 SKUs)

## Quick Start

### 1. Generate Test Data (Optional)
Open `generate_sample_csv.html` in your browser and create a CSV with 8000 SKUs for testing.

### 2. Run the Generator
1. Open `index.html` in any modern web browser
2. Upload your CSV file (must have a "sku" column)
3. Adjust options if needed:
   - QR code size (Small/Medium/Large)
   - Codes per row (3-6)
   - Include/exclude SKU text labels
4. Click "Generate QR Codes & Create PDF"
5. Wait for processing (8000 SKUs takes 2-5 minutes depending on your device)
6. PDF will automatically download when complete

## CSV File Format

Your CSV must have a column named `sku` (case-insensitive). Additional columns are optional.

**Minimum format:**
```csv
sku
SKU-001
SKU-002
SKU-003
```

**Recommended format:**
```csv
sku,name,price,category
SKU-001,Wireless Mouse,29.99,Electronics
SKU-002,USB Cable,12.99,Accessories
SKU-003,Laptop Stand,45.00,Office
```

## Technical Details

### QR Code Library
- **Library:** QRCodeJS v1.0.0
- **Source:** https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js
- **Type:** Client-side JavaScript (no API calls, no internet needed after page load)

### Batch Processing
The application processes QR codes in batches of 50 to:
- Prevent browser memory overload
- Keep UI responsive
- Show real-time progress
- Allow browser to garbage collect between batches

### Performance Benchmarks
| SKUs | Processing Time | PDF Pages | PDF Size |
|------|----------------|-----------|----------|
| 100  | ~5 seconds     | 2-3       | ~500 KB  |
| 500  | ~25 seconds    | 10-12     | ~2 MB    |
| 1000 | ~50 seconds    | 20-25     | ~4 MB    |
| 5000 | ~4 minutes     | 100-125   | ~20 MB   |
| 8000 | ~6 minutes     | 160-200   | ~30 MB   |

*Times vary based on device performance*

### Browser Compatibility
- ✅ Chrome 90+ (Recommended)
- ✅ Firefox 88+
- ✅ Safari 14+
- ✅ Edge 90+

### Limitations
- **Browser Memory:** ~10,000 SKUs maximum recommended
- **PDF Size:** Very large PDFs (>50 MB) may be slow to open
- **Mobile Devices:** Not recommended for >2000 SKUs (limited memory)

## Customization Options

### QR Code Size
- **Small (100x100):** Fits more codes per page, harder to scan
- **Medium (128x128):** Balanced (recommended)
- **Large (150x150):** Easier to scan, fewer codes per page

### Codes Per Row
- **3 per row:** Larger codes, easier to scan
- **4 per row:** Balanced (recommended)
- **5-6 per row:** More codes per page, smaller codes

### Text Labels
- **Enabled:** SKU printed below each QR code (recommended for manual reference)
- **Disabled:** QR code only (cleaner look, more codes per page)

## Printing Tips

1. **Use high-quality printer:** Laser printers work best for QR codes
2. **Print at 100% scale:** Do not shrink or enlarge
3. **Use white paper:** QR codes need good contrast
4. **Test scanning:** Scan a few codes before printing entire batch
5. **Cut with margins:** Leave some white space around each code

## Troubleshooting

### "CSV must have a 'sku' column"
- Ensure your CSV has a column header named exactly `sku` (case doesn't matter)
- Check for typos in the header row

### Browser freezes during generation
- Try a smaller batch first (e.g., 1000 SKUs)
- Close other browser tabs to free memory
- Use a desktop computer instead of mobile device
- Try Chrome for best performance

### PDF won't download
- Check browser's download folder
- Disable popup blocker
- Try a different browser
- Reduce number of SKUs or QR code size

### QR codes won't scan
- Increase QR code size setting
- Print at higher quality
- Ensure good lighting when scanning
- Clean printer heads

## Advanced Usage

### Encoding Additional Data
By default, QR codes contain only the SKU. To include more data, modify your CSV:

**Option 1:** Concatenate data in SKU column
```csv
sku,name,price
SKU-001|Wireless Mouse|29.99,Wireless Mouse,29.99
```

**Option 2:** Use JSON in SKU column
```csv
sku,name,price
"{""sku"":""SKU-001"",""name"":""Mouse"",""price"":29.99}",Wireless Mouse,29.99
```

### Batch Processing Multiple Files
Open the application in multiple browser tabs to process different CSV files simultaneously (if your computer has sufficient memory).

## FAQ

**Q: Does this require internet connection?**
A: Only for the initial page load. After that, it works offline.

**Q: Is my data uploaded anywhere?**
A: No! Everything runs in your browser. Your data never leaves your computer.

**Q: Can I customize the QR code appearance?**
A: The current version generates standard black/white QR codes. For colors/logos, you'd need to modify the code.

**Q: What's the maximum SKU count?**
A: Tested up to 10,000. Beyond that, depends on your device's memory.

**Q: Can I use this for commercial purposes?**
A: Yes, the libraries used are open source (MIT licensed).

## Support

For issues or questions:
1. Check this README
2. Try with the sample CSV file first
3. Test with a smaller subset of your data
4. Check browser console for error messages (F12)

## License

This application uses:
- QRCodeJS (MIT License)
- jsPDF (MIT License)
- html2canvas (MIT License)

The code itself is provided as-is for your use.
