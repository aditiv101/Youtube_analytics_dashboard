# 📊 YouTube Analytics Dashboard - Power BI Project

![Status](https://img.shields.io/badge/Status-Data%20Model%20Complete-success)
![Theme](https://img.shields.io/badge/Theme-YouTube%20Red-red)
![Pages](https://img.shields.io/badge/Pages-5-blue)
![Measures](https://img.shields.io/badge/DAX%20Measures-16-orange)

## 🎯 Project Overview

A comprehensive, multi-page Power BI dashboard analyzing YouTube channel performance with 301 videos. Features a YouTube-inspired red and white theme with interactive visualizations, cross-filtering, and advanced analytics.

### Dataset Information
- **Source**: `orry_youtube_data_FINAL.csv`
- **Records**: 301 videos
- **Date Range**: November 14, 2024 - October 18, 2025
- **Columns**: 7 base columns + 4 calculated columns
- **Measures**: 16 DAX measures
---
## 📸 Dashboard Previews

| Overview | Video Performance | Engagement Insights |
|----------|-------------------|---------------------|
| [![Overview](previews/1_overview.png)](previews/1_overview.png) | [![Video Performance](previews/2_video_performance.png)](previews/2_video_performance.png) | [![Engagement Insights](previews/3_engagement_insights.png)](previews/3_engagement_insights.png) |

| Content Gallery | Settings/About |
|----------------|----------------|
| [![Content Gallery](previews/4_content_gallery.png)](previews/4_content_gallery.png) | [![Settings/About](previews/5_settings_about.png)](previews/5_settings_about.png) |

Click on any image to view full size
---

## ✅ What's Complete

### 🎨 Theme & Design (100%)
- ✅ Custom YouTube theme (`YouTubeTheme.json`)
- ✅ Color palette: Red (#FF0000), White (#FFFFFF), Gray (#E8E8E8)
- ✅ Typography: Segoe UI / Roboto
- ✅ Rounded corners (8px), soft shadows
- ✅ Card-based modern layout

### 📊 Data Model (100%)
- ✅ CSV data imported and transformed
- ✅ **4 Calculated Columns**:
  - `DurationSeconds` (Power Query transformation)
  - `Video Type` (Short/Long classification)
  - `Weekday Name` (Day of week)
  - `Weekday Number` (1-7)

- ✅ **16 DAX Measures**:
  - Core: Total Views, Likes, Comments, Videos
  - Engagement: Engagement Rate, Avg Engagement Rate, Total Engagement
  - Averages: Avg Views, Likes, Comments, Duration per Video
  - Advanced: Views to Likes Ratio, Top 10% Threshold, Short/Long Video Counts

### 📄 Page Structure (100%)
- ✅ Page 1: **Overview Dashboard** - KPIs, trends, top videos
- ✅ Page 2: **Video Performance** - Detailed tables, breakdowns, scatter analysis
- ✅ Page 3: **Engagement Insights** - Trends, top performers, heatmaps
- ✅ Page 4: **Content Gallery** - Image grid with thumbnails
- ✅ Page 5: **Settings / About** - Stats, info, controls

### 📚 Documentation (100%)
- ✅ `DASHBOARD_CONFIGURATION_GUIDE.md` - Complete visual specifications
- ✅ `QUICK_START_GUIDE.md` - Step-by-step implementation
- ✅ `VISUAL_SPECIFICATIONS.json` - Structured visual configs
- ✅ `DAX_MEASURES_REFERENCE.md` - All measures + optional additions
- ✅ `README.md` - This file

---

## 🚀 Quick Start

### Prerequisites
- Power BI Desktop (Latest version)
- Windows OS
- 15 minutes for basic setup
- 60-75 minutes for complete implementation

### Steps to Complete Dashboard

1. **Open Project**
   ```
   File > Open Report > YT.pbip
   ```

2. **Install ChicletSlicer**
   ```
   Insert > Get more visuals > Search "ChicletSlicer" > Add
   ```

3. **Follow Implementation Guide**
   - Open `QUICK_START_GUIDE.md`
   - Follow steps 3-11 for each page
   - Estimated time: 60-75 minutes

4. **Save & Publish**
   ```
   File > Save
   File > Publish to Power BI Service (optional)
   ```

---

## 📋 Page Specifications

### Page 1: Overview Dashboard
**Visuals**: 11 total
- 5 KPI Cards (Views, Likes, Comments, Engagement Rate, Total Videos)
- 1 Line Chart (Views Over Time)
- 1 Donut Chart (Engagement Composition)
- 1 Bar Chart (Top Viewed Videos)
- 1 Table (Recent Videos)
- 2 Slicers (Date Range, Video Type)

### Page 2: Video Performance
**Visuals**: 6 total
- 1 Detailed Table (with conditional formatting)
- 1 Clustered Bar Chart (Performance Breakdown)
- 1 Scatter Chart (Engagement vs Duration)
- 3 Slicers (Date, Video Type, Search)

### Page 3: Engagement Insights
**Visuals**: 7 total
- 1 Combo Chart (Likes, Comments, Views over time)
- 3 Multi-row Cards (Top 3 performers)
- 1 Matrix (Weekday Heatmap)
- 1 Donut Chart (Likes vs Comments)
- 1 Gauge (Avg Engagement Rate)

### Page 4: Content Gallery
**Visuals**: 4 total
- 1 Image Grid (Thumbnails with tooltips)
- 2 Slicers (Video Type, Date Range)
- 1 Card (Video Count)

### Page 5: Settings / About
**Visuals**: 7 total
- 1 Text Box (Dashboard info)
- 3 Cards (Average stats)
- 2 Buttons (Refresh, Dark Mode)
- 1 Image (Channel logo)

---

## 🎨 Design System

### Color Palette
```css
Primary:         #FF0000  /* YouTube Red */
Accent:          #C40000  /* Dark Red */
Background:      #FFFFFF  /* White */
Card BG:         #F8F8F8  /* Off-White */
Secondary:       #E8E8E8  /* Light Gray */
Text:            #222222  /* Dark Gray */
```

### Typography
```
Page Titles:     24px, Segoe UI Semibold
Visual Titles:   14px, Segoe UI Semibold
Body Text:       12px, Segoe UI
Card Values:     24px, Segoe UI
```

### Spacing & Layout
- Canvas: 1280 x 720px
- Grid Padding: 20px
- Border Radius: 8px
- Header Height: 60px
- Navigation Height: 40px

---

## 📊 Key Metrics

### Performance Highlights
- **Total Views**: Sum of all video views
- **Engagement Rate**: (Likes + Comments) / Views
- **Avg Duration**: Average video length in seconds
- **Video Types**: Short (<60s) vs Long (≥60s)

### Top Insights Available
1. Views trending over time
2. Top 10 most viewed videos
3. Engagement rate by video duration
4. Publishing patterns by weekday
5. Short vs Long video performance
6. Recent upload performance

---

## 🔧 Technical Details

### Data Source
```
File: orry_youtube_data_FINAL.csv
Path: D:\aditi projects\bia project\
Format: CSV with headers
Encoding: UTF-8
```

### Power Query Transformations
```m
// Duration Seconds Calculation
let
    dur = Text.AfterDelimiter([video_length], "PT"),
    mins = if Text.Contains(dur, "M") then Number.FromText(Text.BeforeDelimiter(dur, "M")) else 0,
    secsText = if Text.Contains(dur, "S") then 
        (if Text.Contains(dur, "M") then Text.BetweenDelimiters(dur, "M", "S") 
         else Text.BeforeDelimiter(dur, "S")) else "0",
    secs = Number.FromText(Text.Trim(secsText)),
    totalSec = (mins * 60) + secs
in
    totalSec
```

### DAX Patterns Used
- `SUM()` for aggregations
- `DIVIDE()` for safe division
- `CALCULATE()` for context modification
- `AVERAGEX()` for row-level calculations
- `PERCENTILE.INC()` for threshold analysis
- `FORMAT()` for date formatting
- `WEEKDAY()` for day-of-week analysis

---

## 📁 Project Structure

```
bia project/
├── YT.pbip                              # Power BI Project file
├── YT.Report/                           # Report definition
│   ├── definition/
│   │   ├── pages/                       # 5 page folders
│   │   └── report.json                  # Report config
│   └── StaticResources/
│       └── SharedResources/
│           └── BaseThemes/
│               └── YouTubeTheme.json    # Custom theme
├── YT.SemanticModel/                    # Data model
│   └── definition/
│       └── tables/
│           └── orry_youtube_data_FINAL.tmdl  # Table with measures
├── orry_youtube_data_FINAL.csv          # Source data
├── LOGO.png                             # Channel logo
├── *.png                                # Icon images
├── README.md                            # This file
├── DASHBOARD_CONFIGURATION_GUIDE.md     # Detailed specs
├── QUICK_START_GUIDE.md                 # Implementation steps
├── VISUAL_SPECIFICATIONS.json           # Visual configs
└── DAX_MEASURES_REFERENCE.md            # DAX documentation
```

---

## 🎯 Features

### Interactive Elements
- ✅ Cross-filtering across all visuals
- ✅ Drill-through from Overview to Performance
- ✅ Tooltips with thumbnails and key metrics
- ✅ Date range slicers
- ✅ Video type filters
- ✅ Search functionality

### Navigation
- ✅ ChicletSlicer on all pages
- ✅ Horizontal navigation bar
- ✅ Page-to-page navigation
- ✅ Consistent header across pages

### Bookmarks (To Be Created)
- 📌 "Top 5 Videos" - Filter to top performers
- 📌 "Recent Uploads" - Last 30 days

### Advanced Features
- Conditional formatting (gradients, data bars)
- Heatmap visualization
- Scatter plot analysis
- Combo charts
- Image grid with dynamic borders

---

## 📈 Analytics Capabilities

### Questions This Dashboard Answers

1. **Performance**
   - Which videos get the most views?
   - What's the average engagement rate?
   - How do short vs long videos perform?

2. **Trends**
   - How are views trending over time?
   - Which day of week gets most uploads?
   - Is engagement improving or declining?

3. **Content Strategy**
   - What video length performs best?
   - Which videos drive most engagement?
   - What's the optimal posting frequency?

4. **Engagement**
   - What's the likes-to-views ratio?
   - How many comments per video?
   - Which videos spark most discussion?

---

## 🛠️ Customization Options

### Easy Modifications
1. **Change Colors**: Edit `YouTubeTheme.json`
2. **Add Measures**: Use `DAX_MEASURES_REFERENCE.md`
3. **Adjust Layouts**: Modify visual positions
4. **Add Filters**: Insert new slicers
5. **Change Data Source**: Update Power Query connection

### Advanced Customization
1. Add custom visuals from AppSource
2. Create calculated tables for complex analysis
3. Implement row-level security
4. Add R/Python visuals
5. Create custom tooltips

---

## 📊 Data Dictionary

### Base Columns
| Column | Type | Description |
|--------|------|-------------|
| `video_name` | Text | Title of the video |
| `publish_date` | DateTime | Publication timestamp |
| `sum_of_views` | Integer | Total view count |
| `sum_of_likes` | Integer | Total like count |
| `sum_of_comments` | Integer | Total comment count |
| `video_length` | Text | Duration in ISO 8601 format (PT#M#S) |
| `thumbnail_url` | Text | URL to video thumbnail image |

### Calculated Columns
| Column | Type | Formula | Description |
|--------|------|---------|-------------|
| `DurationSeconds` | Integer | Power Query | Video length in seconds |
| `Video Type` | Text | IF(<60, "Short", "Long") | Classification |
| `Weekday Name` | Text | FORMAT(date, "dddd") | Day name |
| `Weekday Number` | Integer | WEEKDAY(date, 2) | 1=Mon, 7=Sun |

---

## 🐛 Troubleshooting

### Common Issues

**Issue**: Theme not applied
```
Solution: View > Themes > Browse > Select YouTubeTheme.json
```

**Issue**: Measures not visible
```
Solution: Refresh Fields pane or reopen Power BI Desktop
```

**Issue**: Images not displaying
```
Solution: Set thumbnail_url data category to "Image URL"
```

**Issue**: ChicletSlicer not found
```
Solution: Insert > Get more visuals > Search and install
```

**Issue**: Navigation not working
```
Solution: ChicletSlicer > Format > Action > Page navigation
```

---

## 📚 Resources

### Documentation Files
1. **QUICK_START_GUIDE.md** - Start here for implementation
2. **DASHBOARD_CONFIGURATION_GUIDE.md** - Detailed specifications
3. **VISUAL_SPECIFICATIONS.json** - Structured visual configs
4. **DAX_MEASURES_REFERENCE.md** - All DAX formulas

### External Resources
- [Power BI Documentation](https://docs.microsoft.com/power-bi/)
- [DAX Guide](https://dax.guide/)
- [Power BI Community](https://community.powerbi.com/)
- [ChicletSlicer Documentation](https://appsource.microsoft.com/)

---

## ✅ Completion Checklist

### Data Model
- [x] CSV imported
- [x] Columns transformed
- [x] Calculated columns created
- [x] DAX measures created
- [x] Relationships configured

### Theme & Design
- [x] Custom theme created
- [x] Colors defined
- [x] Typography specified
- [x] Layout guidelines set

### Documentation
- [x] Configuration guide
- [x] Quick start guide
- [x] Visual specifications
- [x] DAX reference
- [x] README

### Implementation (To Do in Power BI Desktop)
- [ ] Open project in Power BI Desktop
- [ ] Install ChicletSlicer
- [ ] Configure Page 1: Overview
- [ ] Configure Page 2: Performance
- [ ] Configure Page 3: Engagement
- [ ] Configure Page 4: Gallery
- [ ] Configure Page 5: Settings
- [ ] Add navigation to all pages
- [ ] Configure interactions
- [ ] Create bookmarks
- [ ] Test functionality
- [ ] Save and publish

---

## 🎓 Learning Outcomes

By completing this dashboard, you'll learn:
- ✅ Power BI project structure (.pbip)
- ✅ Custom theme creation
- ✅ DAX measure development
- ✅ Power Query transformations
- ✅ Visual configuration and formatting
- ✅ Interactive dashboard design
- ✅ Cross-filtering and drill-through
- ✅ Bookmark creation
- ✅ Mobile layout optimization

---

## 📞 Support

For questions or issues:
1. Check the troubleshooting section above
2. Review the documentation files
3. Consult Power BI official documentation
4. Search Power BI Community forums

---

## 📄 License

This dashboard template is provided as-is for educational and analytical purposes.

---

## 🎉 Credits

**Data Source**: YouTube channel analytics (orry_youtube_data_FINAL.csv)
**Design**: YouTube-inspired theme
**Tools**: Power BI Desktop, DAX, Power Query
**Documentation**: Comprehensive guides and references

---

## 🚀 Next Steps

1. **Immediate**: Open `QUICK_START_GUIDE.md` and start building
2. **Short-term**: Complete all 5 pages following the guide
3. **Medium-term**: Customize colors, add custom measures
4. **Long-term**: Publish to Power BI Service, create mobile layout

---

**Status**: ✅ Data Model Complete | 📋 Ready for Visual Configuration

**Estimated Time to Complete**: 60-75 minutes

**Start Building**: Open `QUICK_START_GUIDE.md` now! 🚀

---

*Last Updated: October 19, 2025*
*Version: 1.0*
*Project Type: Power BI Analytics Dashboard*
