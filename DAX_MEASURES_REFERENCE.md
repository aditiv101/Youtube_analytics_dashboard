# DAX Measures Reference - YouTube Analytics Dashboard

## ✅ Already Created Measures

All these measures are already in your data model and ready to use:

### 1. Core Aggregations
```dax
Total Views = SUM('orry_youtube_data_FINAL'[sum_of_views])
```

```dax
Total Likes = SUM('orry_youtube_data_FINAL'[sum_of_likes])
```

```dax
Total Comments = SUM('orry_youtube_data_FINAL'[sum_of_comments])
```

```dax
Total Videos = COUNTROWS('orry_youtube_data_FINAL')
```

### 2. Engagement Metrics
```dax
Engagement Rate = 
DIVIDE(
    SUM('orry_youtube_data_FINAL'[sum_of_likes]) + SUM('orry_youtube_data_FINAL'[sum_of_comments]), 
    SUM('orry_youtube_data_FINAL'[sum_of_views])
)
```

```dax
Avg Engagement Rate = 
AVERAGEX(
    'orry_youtube_data_FINAL', 
    DIVIDE([sum_of_likes] + [sum_of_comments], [sum_of_views], 0)
)
```

```dax
Total Engagement = [Total Likes] + [Total Comments]
```

### 3. Averages
```dax
Avg Views per Video = AVERAGE('orry_youtube_data_FINAL'[sum_of_views])
```

```dax
Avg Likes per Video = AVERAGE('orry_youtube_data_FINAL'[sum_of_likes])
```

```dax
Avg Comments per Video = AVERAGE('orry_youtube_data_FINAL'[sum_of_comments])
```

```dax
Avg Duration (Seconds) = AVERAGE('orry_youtube_data_FINAL'[DurationSeconds])
```

### 4. Ratios & Comparisons
```dax
Views to Likes Ratio = DIVIDE([Total Views], [Total Likes], 0)
```

```dax
Top 10% Engagement Threshold = 
PERCENTILE.INC(ALL('orry_youtube_data_FINAL'[sum_of_likes]), 0.9)
```

### 5. Video Type Counts
```dax
Short Videos Count = 
CALCULATE([Total Videos], 'orry_youtube_data_FINAL'[Video Type] = "Short")
```

```dax
Long Videos Count = 
CALCULATE([Total Videos], 'orry_youtube_data_FINAL'[Video Type] = "Long")
```

---

## 📊 Already Created Calculated Columns

### 1. Duration in Seconds
```dax
DurationSeconds = 
// Calculated in Power Query, available as column
```

### 2. Video Type Classification
```dax
Video Type = IF([DurationSeconds] < 60, "Short", "Long")
```

### 3. Weekday Information
```dax
Weekday Name = FORMAT([publish_date], "dddd")
```

```dax
Weekday Number = WEEKDAY([publish_date], 2)
```

---

## 🆕 Optional Additional Measures

If you need more advanced analytics, here are additional measures you can create:

### Time Intelligence

#### Month-over-Month Growth
```dax
MoM Views Growth % = 
VAR CurrentMonth = [Total Views]
VAR PreviousMonth = 
    CALCULATE(
        [Total Views],
        DATEADD('orry_youtube_data_FINAL'[publish_date], -1, MONTH)
    )
RETURN
    DIVIDE(CurrentMonth - PreviousMonth, PreviousMonth, 0)
```

#### Year-to-Date Views
```dax
YTD Views = 
TOTALYTD(
    [Total Views],
    'orry_youtube_data_FINAL'[publish_date]
)
```

#### Last 30 Days Views
```dax
Last 30 Days Views = 
CALCULATE(
    [Total Views],
    DATESINPERIOD(
        'orry_youtube_data_FINAL'[publish_date],
        LASTDATE('orry_youtube_data_FINAL'[publish_date]),
        -30,
        DAY
    )
)
```

### Performance Rankings

#### Video Rank by Views
```dax
Video Rank = 
RANKX(
    ALL('orry_youtube_data_FINAL'[video_name]),
    [Total Views],
    ,
    DESC,
    DENSE
)
```

#### Top Performer Indicator
```dax
Is Top 10 Video = 
IF([Video Rank] <= 10, "Yes", "No")
```

#### Percentile Rank
```dax
Engagement Percentile = 
PERCENTILEX.INC(
    ALL('orry_youtube_data_FINAL'),
    [Engagement Rate]
)
```

### Engagement Analysis

#### Like Rate
```dax
Like Rate = DIVIDE([Total Likes], [Total Views], 0)
```

#### Comment Rate
```dax
Comment Rate = DIVIDE([Total Comments], [Total Views], 0)
```

#### Engagement Score (Weighted)
```dax
Engagement Score = 
([Total Likes] * 1) + ([Total Comments] * 2)
// Comments weighted 2x as they indicate higher engagement
```

#### Viral Threshold
```dax
Is Viral = 
IF([Total Views] > 100000, "Viral", "Normal")
```

### Duration Analysis

#### Avg Duration (Minutes)
```dax
Avg Duration (Minutes) = 
DIVIDE([Avg Duration (Seconds)], 60, 0)
```

#### Duration Category
```dax
Duration Category = 
SWITCH(
    TRUE(),
    [DurationSeconds] < 30, "Ultra Short (<30s)",
    [DurationSeconds] < 60, "Short (30-60s)",
    [DurationSeconds] < 180, "Medium (1-3min)",
    [DurationSeconds] < 600, "Long (3-10min)",
    "Very Long (>10min)"
)
```

### Comparative Metrics

#### Views vs Average
```dax
Views vs Avg = 
[Total Views] - [Avg Views per Video]
```

#### Performance Index
```dax
Performance Index = 
DIVIDE(
    [Total Views],
    [Avg Views per Video],
    0
)
// >1 = Above average, <1 = Below average
```

#### Engagement vs Benchmark
```dax
Engagement vs Benchmark = 
VAR Benchmark = 0.03  // 3% benchmark
RETURN
    [Engagement Rate] - Benchmark
```

### Content Mix Analysis

#### Short Video %
```dax
Short Video % = 
DIVIDE([Short Videos Count], [Total Videos], 0)
```

#### Long Video %
```dax
Long Video % = 
DIVIDE([Long Videos Count], [Total Videos], 0)
```

#### Avg Views by Video Type
```dax
Avg Views (Short) = 
CALCULATE(
    [Avg Views per Video],
    'orry_youtube_data_FINAL'[Video Type] = "Short"
)
```

```dax
Avg Views (Long) = 
CALCULATE(
    [Avg Views per Video],
    'orry_youtube_data_FINAL'[Video Type] = "Long"
)
```

### Trend Analysis

#### Moving Average (7 days)
```dax
7-Day Moving Avg Views = 
AVERAGEX(
    DATESINPERIOD(
        'orry_youtube_data_FINAL'[publish_date],
        LASTDATE('orry_youtube_data_FINAL'[publish_date]),
        -7,
        DAY
    ),
    [Total Views]
)
```

#### Growth Rate
```dax
Growth Rate = 
VAR FirstValue = 
    CALCULATE(
        [Total Views],
        FIRSTDATE('orry_youtube_data_FINAL'[publish_date])
    )
VAR LastValue = 
    CALCULATE(
        [Total Views],
        LASTDATE('orry_youtube_data_FINAL'[publish_date])
    )
RETURN
    DIVIDE(LastValue - FirstValue, FirstValue, 0)
```

### Best/Worst Performers

#### Best Performing Video
```dax
Best Video = 
CALCULATE(
    SELECTEDVALUE('orry_youtube_data_FINAL'[video_name]),
    TOPN(1, ALL('orry_youtube_data_FINAL'), [Total Views], DESC)
)
```

#### Worst Performing Video
```dax
Worst Video = 
CALCULATE(
    SELECTEDVALUE('orry_youtube_data_FINAL'[video_name]),
    TOPN(1, ALL('orry_youtube_data_FINAL'), [Total Views], ASC)
)
```

#### Best Engagement Video
```dax
Best Engagement Video = 
CALCULATE(
    SELECTEDVALUE('orry_youtube_data_FINAL'[video_name]),
    TOPN(1, ALL('orry_youtube_data_FINAL'), [Engagement Rate], DESC)
)
```

### Publishing Pattern Analysis

#### Videos This Week
```dax
Videos This Week = 
CALCULATE(
    [Total Videos],
    DATESBETWEEN(
        'orry_youtube_data_FINAL'[publish_date],
        TODAY() - 7,
        TODAY()
    )
)
```

#### Most Active Weekday
```dax
Most Active Weekday = 
VAR MaxCount = 
    MAXX(
        VALUES('orry_youtube_data_FINAL'[Weekday Name]),
        CALCULATE([Total Videos])
    )
RETURN
    CALCULATE(
        SELECTEDVALUE('orry_youtube_data_FINAL'[Weekday Name]),
        FILTER(
            VALUES('orry_youtube_data_FINAL'[Weekday Name]),
            [Total Videos] = MaxCount
        )
    )
```

### Conditional Formatting Helpers

#### Views Color
```dax
Views Color = 
SWITCH(
    TRUE(),
    [Total Views] >= 1000000, "#FF0000",  // Red for 1M+
    [Total Views] >= 100000, "#FF6B6B",   // Light red for 100K+
    [Total Views] >= 10000, "#FFA07A",    // Lighter red for 10K+
    "#E8E8E8"                              // Gray for rest
)
```

#### Engagement Status
```dax
Engagement Status = 
SWITCH(
    TRUE(),
    [Engagement Rate] >= 0.05, "Excellent",
    [Engagement Rate] >= 0.03, "Good",
    [Engagement Rate] >= 0.01, "Average",
    "Needs Improvement"
)
```

---

## 🎯 How to Add New Measures

### In Power BI Desktop:
1. Go to **Data** view or **Model** view
2. Select the `orry_youtube_data_FINAL` table
3. Click **New Measure** in the ribbon
4. Copy-paste the DAX code
5. Press **Enter**
6. The measure appears in the Fields pane

### In .pbip Project (Advanced):
1. Open `YT.SemanticModel\definition\tables\orry_youtube_data_FINAL.tmdl`
2. Add measure before the `partition` section:
```
measure 'Measure Name' = <DAX Formula>
    formatString: <format>
```
3. Save the file
4. Reopen in Power BI Desktop

---

## 📐 Format Strings Reference

Use these in your measures:

```dax
formatString: 0                    // Whole number: 12345
formatString: #,##0                // Thousands separator: 12,345
formatString: 0.00                 // Two decimals: 123.45
formatString: 0.00%                // Percentage: 12.34%
formatString: $#,##0.00            // Currency: $12,345.67
formatString: "Short Date"         // Date: 1/15/2024
formatString: "Long Date"          // Date: January 15, 2024
formatString: "General Number"     // Auto format
```

---

## 🔍 Testing Your Measures

### Quick Test:
1. Create a **Card** visual
2. Drag your measure to it
3. Check if the value makes sense
4. Try filtering by Video Type or Date
5. Verify the calculation updates correctly

### Common Issues:
- **BLANK result**: Check for division by zero, use DIVIDE with default value
- **Wrong total**: Use SUMX or AVERAGEX instead of SUM/AVERAGE
- **Circular dependency**: Measures can't reference themselves
- **Context error**: Use CALCULATE to change filter context

---

## 💡 Pro Tips

1. **Name measures clearly**: Use spaces and proper capitalization
2. **Add comments**: Use `//` for inline comments in DAX
3. **Format consistently**: Always add formatString
4. **Test edge cases**: What if no data? What if filter returns nothing?
5. **Use variables**: VAR makes complex measures readable
6. **Avoid calculated columns for aggregations**: Use measures instead
7. **Document complex logic**: Add description in measure properties

---

## 📚 DAX Functions Used

### Aggregation
- `SUM()` - Sum of column
- `AVERAGE()` - Average of column
- `COUNT()` - Count rows
- `COUNTROWS()` - Count rows in table

### Statistical
- `PERCENTILE.INC()` - Percentile value
- `RANKX()` - Rank values
- `TOPN()` - Top N rows

### Filter
- `CALCULATE()` - Modify filter context
- `FILTER()` - Filter table
- `ALL()` - Remove filters
- `VALUES()` - Unique values

### Time Intelligence
- `DATEADD()` - Shift dates
- `DATESINPERIOD()` - Date range
- `TOTALYTD()` - Year-to-date
- `LASTDATE()` - Last date in context

### Logical
- `IF()` - Conditional
- `SWITCH()` - Multiple conditions
- `DIVIDE()` - Safe division

### Iterator
- `SUMX()` - Row-by-row sum
- `AVERAGEX()` - Row-by-row average
- `MAXX()` - Row-by-row maximum

---

## ✅ Measure Checklist

Before deploying a measure:
- [ ] Tested with sample data
- [ ] Handles BLANK/NULL values
- [ ] Format string applied
- [ ] Name is clear and descriptive
- [ ] Works with all filters
- [ ] Performance is acceptable
- [ ] Documented if complex

---

**All 16 core measures are already in your model. Use this reference to add more as needed!**
