# YouTube Analytics Dashboard - Complete Configuration Guide

## ✅ COMPLETED: Data Model Setup

### Measures Created:
- ✅ Total Views = SUM('orry_youtube_data_FINAL'[sum_of_views])
- ✅ Total Likes = SUM('orry_youtube_data_FINAL'[sum_of_likes])
- ✅ Total Comments = SUM('orry_youtube_data_FINAL'[sum_of_comments])
- ✅ Engagement Rate = DIVIDE(SUM('orry_youtube_data_FINAL'[sum_of_likes]) + SUM('orry_youtube_data_FINAL'[sum_of_comments]), SUM('orry_youtube_data_FINAL'[sum_of_views]))
- ✅ Total Videos = COUNTROWS('orry_youtube_data_FINAL')
- ✅ Avg Likes per Video = AVERAGE('orry_youtube_data_FINAL'[sum_of_likes])
- ✅ Avg Comments per Video = AVERAGE('orry_youtube_data_FINAL'[sum_of_comments])
- ✅ Avg Duration (Seconds) = AVERAGE('orry_youtube_data_FINAL'[DurationSeconds])

### Calculated Columns Created:
- ✅ DurationSeconds (via Power Query)
- ✅ Video Type = IF([DurationSeconds] < 60, "Short", "Long")

### ✅ Theme Applied:
- Custom YouTube theme with Red (#FF0000) and White (#FFFFFF) color scheme
- Theme file: YouTubeTheme.json

---

## 📋 PAGE 1: OVERVIEW DASHBOARD

### Page Settings:
- **Name**: Overview
- **Display Name**: "Overview Dashboard"
- **Canvas Size**: 1280 x 720
- **Background**: White (#FFFFFF)

### Header Bar (All Pages):
- **Type**: Rectangle Shape
- **Position**: X=0, Y=0
- **Size**: Width=1280, Height=60
- **Fill Color**: #FF0000
- **Text**: "YouTube Dashboard" (White, 24px, Segoe UI Semibold)

### Top Navigation (ChicletSlicer) - Position on all pages:
- **Visual Type**: ChicletSlicer (Custom Visual - Version 2.2.1.0)
- **Position**: X=150, Y=10
- **Size**: Width=900, Height=40
- **Values**: Overview, Performance, Engagement, Gallery, Settings
- **Configuration**:
  - Background: White
  - Selected Color: Red (#FF0000)
  - Text Color: Black (#222222)
  - Orientation: Horizontal
  - Shape: Rounded rectangle
  - Action: Page Navigation

### Visual 1: KPI Card - Total Views
- **Visual Type**: Card
- **Position**: X=20, Y=80
- **Size**: Width=180, Height=100
- **Field**: [Total Views]
- **Format**:
  - Background: #F8F8F8
  - Title: "Total Views" (Red #FF0000, 12px bold)
  - Value: 24px, Black
  - Border Radius: 8px

### Visual 2: KPI Card - Total Likes
- **Position**: X=220, Y=80
- **Size**: Width=180, Height=100
- **Field**: [Total Likes]
- **Format**: Same as Total Views

### Visual 3: KPI Card - Total Comments
- **Position**: X=420, Y=80
- **Size**: Width=180, Height=100
- **Field**: [Total Comments]
- **Format**: Same as Total Views

### Visual 4: KPI Card - Engagement Rate
- **Position**: X=620, Y=80
- **Size**: Width=180, Height=100
- **Field**: [Engagement Rate]
- **Format**: Same as Total Views (Display as percentage)

### Visual 5: KPI Card - Total Videos
- **Position**: X=820, Y=80
- **Size**: Width=180, Height=100
- **Field**: [Total Videos]
- **Format**: Same as Total Views

### Visual 6: Line Chart - Views Over Time
- **Visual Type**: Line Chart
- **Position**: X=20, Y=200
- **Size**: Width=600, Height=250
- **X-Axis**: publish_date
- **Y-Axis**: [Total Views]
- **Title**: "Views Over Time"
- **Format**:
  - Line Color: Red (#FF0000)
  - Background: White
  - Border Radius: 8px

### Visual 7: Donut Chart - Engagement Composition
- **Visual Type**: Donut Chart
- **Position**: X=640, Y=200
- **Size**: Width=300, Height=250
- **Legend**: Likes, Comments, Views
- **Values**: [Total Likes], [Total Comments], [Total Views]
- **Title**: "Engagement Composition"
- **Colors**: Red shades (#FF0000, #C40000, #E8E8E8)

### Visual 8: Bar Chart - Top Viewed Videos
- **Visual Type**: Clustered Bar Chart
- **Position**: X=960, Y=200
- **Size**: Width=300, Height=250
- **Axis**: video_name
- **Values**: [Total Views]
- **Sort**: Descending by Total Views
- **Title**: "Top Viewed Videos"
- **Top N**: 10 videos

### Visual 9: Table - Recent Videos
- **Visual Type**: Table
- **Position**: X=20, Y=470
- **Size**: Width=700, Height=230
- **Columns**: 
  - video_name
  - [Total Views]
  - [Total Likes]
  - [Total Comments]
  - [Video Type]
- **Sort**: publish_date (Descending)
- **Top N**: 5 rows

### Visual 10: Slicer - Date Range
- **Visual Type**: Slicer (Date Range)
- **Position**: X=740, Y=470
- **Size**: Width=250, Height=100
- **Field**: publish_date
- **Style**: Between

### Visual 11: Slicer - Video Type
- **Visual Type**: Slicer (Dropdown)
- **Position**: X=1010, Y=470
- **Size**: Width=250, Height=100
- **Field**: [Video Type]
- **Style**: Dropdown

---

## 📋 PAGE 2: VIDEO PERFORMANCE

### Page Settings:
- **Name**: Performance
- **Display Name**: "Video Performance"
- **Canvas Size**: 1280 x 720
- **Background**: White (#FFFFFF)

### Visual 1: Table - Detailed Performance
- **Visual Type**: Table
- **Position**: X=20, Y=80
- **Size**: Width=800, Height=400
- **Columns**:
  - video_name
  - publish_date
  - [Total Views]
  - [Total Likes]
  - [Total Comments]
  - [Engagement Rate]
  - DurationSeconds
- **Conditional Formatting**:
  - [Total Views]: Red gradient (light to dark)
  - [Engagement Rate]: Data bars (Red)

### Visual 2: Clustered Bar Chart - Performance Breakdown
- **Visual Type**: Clustered Bar Chart
- **Position**: X=840, Y=80
- **Size**: Width=420, Height=300
- **Axis**: video_name (Top 10)
- **Values**: [Total Views], [Total Likes], [Total Comments]
- **Title**: "Video Performance Breakdown"
- **Colors**: Red (#FF0000), Dark Red (#C40000), Gray (#E8E8E8)

### Visual 3: Scatter Chart - Engagement vs Duration
- **Visual Type**: Scatter Chart
- **Position**: X=840, Y=400
- **Size**: Width=420, Height=300
- **X-Axis**: DurationSeconds
- **Y-Axis**: [Engagement Rate]
- **Size**: [Total Views]
- **Title**: "Engagement vs Duration"
- **Color**: Red (#FF0000)

### Visual 4: Slicer - Date Range
- **Position**: X=20, Y=500
- **Size**: Width=250, Height=80
- **Field**: publish_date

### Visual 5: Slicer - Video Type
- **Position**: X=290, Y=500
- **Size**: Width=250, Height=80
- **Field**: [Video Type]

### Visual 6: Slicer - Video Search
- **Position**: X=560, Y=500
- **Size**: Width=250, Height=80
- **Field**: video_name
- **Style**: Search

---

## 📋 PAGE 3: ENGAGEMENT INSIGHTS

### Page Settings:
- **Name**: Engagement
- **Display Name**: "Engagement Insights"
- **Canvas Size**: 1280 x 720
- **Background**: White (#FFFFFF)

### Visual 1: Line and Clustered Column Chart
- **Visual Type**: Line and Clustered Column Chart
- **Position**: X=20, Y=80
- **Size**: Width=800, Height=300
- **Axis**: publish_date
- **Column Values**: [Total Likes], [Total Comments]
- **Line Values**: [Total Views]
- **Title**: "Engagement Trends Over Time"
- **Colors**: Red (#FF0000), Dark Red (#C40000) for columns, Black line

### Visual 2: Card - Top Video #1
- **Visual Type**: Multi-row Card
- **Position**: X=840, Y=80
- **Size**: Width=420, Height=90
- **Fields**: video_name, [Engagement Rate]
- **Filter**: Top 1 by Engagement Rate
- **Title**: "🥇 Top Performing Video"

### Visual 3: Card - Top Video #2
- **Position**: X=840, Y=180
- **Size**: Width=420, Height=90
- **Filter**: Top 2 by Engagement Rate (show 2nd)
- **Title**: "🥈 Second Best"

### Visual 4: Card - Top Video #3
- **Position**: X=840, Y=280
- **Size**: Width=420, Height=90
- **Filter**: Top 3 by Engagement Rate (show 3rd)
- **Title**: "🥉 Third Place"

### Visual 5: Matrix - Engagement Heatmap
- **Visual Type**: Matrix
- **Position**: X=20, Y=400
- **Size**: Width=500, Height=300
- **Rows**: WEEKDAY(publish_date) - Custom column needed
- **Columns**: Metric (Likes, Comments)
- **Values**: SUM
- **Conditional Formatting**: Color scale (White to Red)

### Visual 6: Donut Chart - Likes vs Comments
- **Visual Type**: Donut Chart
- **Position**: X=540, Y=400
- **Size**: Width=300, Height=300
- **Legend**: Likes, Comments
- **Values**: [Total Likes], [Total Comments]
- **Title**: "Engagement Split"
- **Colors**: Red (#FF0000), Dark Red (#C40000)

### Visual 7: Gauge - Average Engagement Rate
- **Visual Type**: Gauge
- **Position**: X=860, Y=400
- **Size**: Width=400, Height=300
- **Value**: [Engagement Rate]
- **Target**: 0.05 (5%)
- **Colors**: Red gradient

---

## 📋 PAGE 4: CONTENT GALLERY

### Page Settings:
- **Name**: Gallery
- **Display Name**: "Content Gallery"
- **Canvas Size**: 1280 x 720
- **Background**: White (#FFFFFF)

### Visual 1: Image Grid
- **Visual Type**: Custom Visual - Image Grid or Table with Images
- **Position**: X=20, Y=80
- **Size**: Width=1000, Height=620
- **Field**: thumbnail_url
- **Tooltip Fields**:
  - video_name
  - [Total Views]
  - [Total Likes]
  - DurationSeconds
- **Layout**: 4 columns per row
- **Border**: Red (#FF0000) for top 10% engagement videos

### Visual 2: Slicer - Video Type
- **Position**: X=1040, Y=80
- **Size**: Width=220, Height=100
- **Field**: [Video Type]

### Visual 3: Slicer - Date Range
- **Position**: X=1040, Y=200
- **Size**: Width=220, Height=100
- **Field**: publish_date

### Visual 4: Card - Selected Video Count
- **Position**: X=1040, Y=320
- **Size**: Width=220, Height=80
- **Field**: [Total Videos]
- **Title**: "Videos Shown"

---

## 📋 PAGE 5: SETTINGS / ABOUT

### Page Settings:
- **Name**: Settings
- **Display Name**: "Settings / About"
- **Canvas Size**: 1280 x 720
- **Background**: White (#FFFFFF)

### Visual 1: Text Box - Dashboard Info
- **Visual Type**: Text Box
- **Position**: X=100, Y=100
- **Size**: Width=1080, Height=100
- **Text**: "YouTube Analytics Dashboard – Created in Power BI"
- **Font**: Roboto Bold, 16px
- **Color**: #222222
- **Alignment**: Center

### Visual 2: Card - Avg Likes per Video
- **Position**: X=100, Y=230
- **Size**: Width=300, Height=120
- **Field**: [Avg Likes per Video]
- **Title**: "Average Likes per Video"

### Visual 3: Card - Avg Comments per Video
- **Position**: X=490, Y=230
- **Size**: Width=300, Height=120
- **Field**: [Avg Comments per Video]
- **Title**: "Average Comments per Video"

### Visual 4: Card - Avg Duration
- **Position**: X=880, Y=230
- **Size**: Width=300, Height=120
- **Field**: [Avg Duration (Seconds)]
- **Title**: "Average Video Duration (sec)"

### Visual 5: Button - Refresh Data
- **Visual Type**: Button
- **Position**: X=400, Y=400
- **Size**: Width=200, Height=60
- **Text**: "Refresh Data"
- **Action**: Refresh
- **Style**: 
  - Background: Red (#FF0000)
  - Text: White
  - Border Radius: 8px

### Visual 6: Button - Dark Mode Toggle
- **Position**: X=680, Y=400
- **Size**: Width=200, Height=60
- **Text**: "Dark Mode"
- **Action**: Bookmark Toggle
- **Style**: Same as Refresh button

### Visual 7: Image - Channel Logo
- **Position**: X=540, Y=500
- **Size**: Width=200, Height=150
- **Image**: LOGO.png (from project folder)

---

## 🎨 GLOBAL FORMATTING APPLIED

### Color Palette:
- Primary: #FF0000 (Red)
- Secondary: #E8E8E8 (Light Gray)
- Text: #222222 (Dark Gray)
- Background: #FFFFFF (White)
- Card Background: #F8F8F8 (Off-White)
- Accent: #C40000 (Dark Red)

### Typography:
- Page Titles: 24px, Segoe UI Semibold
- Visual Titles: 14px, Segoe UI Semibold
- Body Text: 12px, Segoe UI
- Card Values: 24px, Segoe UI

### Visual Styling:
- Border Radius: 8px on all cards and visuals
- Shadow: Soft gray shadow on cards
- Padding: 20px grid spacing

---

## 🔧 INTERACTIONS & NAVIGATION

### Cross-Filtering:
- ✅ Enable cross-filtering on all visuals within each page
- Slicers affect all visuals on the page

### Drill-Through:
- From Overview → Video Performance → Individual Video details
- Context: video_name

### Tooltips:
- All visuals include:
  - thumbnail_url (image)
  - video_name
  - [Total Views]
  - [Engagement Rate]

### Bookmarks:
1. **"Top 5 Videos"**: Filter to show top 5 by views
2. **"Recent Uploads"**: Filter to last 30 days

---

## 📝 IMPLEMENTATION NOTES

### Custom Visuals Required:
1. **ChicletSlicer** (Version 2.2.1.0)
   - Download from AppSource
   - Used for page navigation

2. **Image Grid** (Optional)
   - For Content Gallery page
   - Alternative: Use Table visual with image URLs

### Additional DAX Measures Needed:
```dax
// For Engagement Insights - Weekday
Weekday Name = FORMAT([publish_date], "dddd")

// For conditional formatting
Top 10% Engagement = 
VAR CurrentEngagement = [Engagement Rate]
VAR Percentile90 = PERCENTILE.INC(ALL('orry_youtube_data_FINAL'[Engagement Rate]), 0.9)
RETURN IF(CurrentEngagement >= Percentile90, 1, 0)
```

### Power Query Transformations:
- ✅ DurationSeconds already created
- Date table auto-generated by Power BI

---

## ✅ COMPLETION CHECKLIST

- [x] Data model with all measures
- [x] Calculated columns (DurationSeconds, Video Type)
- [x] Custom YouTube theme applied
- [x] 5 pages created with proper names
- [ ] Page 1: Overview - All visuals configured
- [ ] Page 2: Performance - All visuals configured
- [ ] Page 3: Engagement - All visuals configured
- [ ] Page 4: Gallery - All visuals configured
- [ ] Page 5: Settings - All visuals configured
- [ ] ChicletSlicer navigation on all pages
- [ ] Cross-filtering enabled
- [ ] Drill-through configured
- [ ] Bookmarks created
- [ ] Tooltips configured

---

## 🚀 NEXT STEPS TO COMPLETE IN POWER BI DESKTOP

1. **Open the .pbip project** in Power BI Desktop
2. **Install ChicletSlicer** from AppSource (Insert > Get more visuals)
3. **Configure each page** following the specifications above
4. **Add the navigation ChicletSlicer** to all pages
5. **Set up interactions** (Format > Edit interactions)
6. **Create bookmarks** (View > Bookmarks pane)
7. **Configure drill-through** (Right-click page > Drill through)
8. **Test all functionality**
9. **Publish to Power BI Service** (optional)

---

## 📊 DATASET SUMMARY

- **Total Records**: 301 videos
- **Date Range**: 2024-11-14 to 2025-10-18
- **Columns**: 7 (video_name, publish_date, sum_of_views, sum_of_likes, sum_of_comments, video_length, thumbnail_url)
- **Calculated Columns**: 2 (DurationSeconds, Video Type)
- **Measures**: 8

---

**Dashboard Status**: ✅ Data Model Complete | 🎨 Theme Applied | 📋 Configuration Guide Ready

**To complete**: Open in Power BI Desktop and configure visuals following this guide.
