# 🏨 Hotel Booking Analysis --- Power BI Dashboard

> An interactive, single-page Power BI dashboard for exploring hotel
> booking demand, cancellations, customer repeat status, and market
> segments.

------------------------------------------------------------------------

## 📌 Project Overview

This project analyzes the **Hotel Booking Demand** dataset using Power
BI.

The goal was to build a concise, business-oriented dashboard that
focuses on the most useful patterns in the booking data without
overcrowding the report with unnecessary visuals.

The final dashboard combines summary Cards, interactive filters, and
four main analytical visuals on a **single Power BI page**.

------------------------------------------------------------------------

## 🎯 Business Focus

The dashboard focuses on four core areas:

-   📈 **Booking Demand Over Time**
-   ❌ **Cancellation Analysis**
-   👤 **Customer Repeat Status**
-   📊 **Market Segment Analysis**

The dashboard also provides high-level summary Cards for the main
numerical measures.

------------------------------------------------------------------------

## 📊 Dataset

The project uses the **Hotel Booking Demand** dataset, which contains
booking records from two hotel properties:

-   **City Hotel**
-   **Resort Hotel**

The original dataset contains approximately **119,000 booking records**
and **32 variables**.

Important fields include:

-   Hotel
-   Cancellation status
-   Lead time
-   Length of stay
-   Market segment
-   Distribution channel
-   Customer type
-   Repeat guest status
-   Average Daily Rate
-   Reservation status
-   Special requests

------------------------------------------------------------------------

## 🧹 Data Cleaning & Preparation

Data preparation was performed before building the dashboard.

Main preparation steps included:

-   Removing exact duplicate rows across all available columns
-   Handling `NA` values in the `children` field
-   Converting fields to appropriate data types
-   Creating a month-number field to support chronological month
    ordering

After removing exact duplicate rows, the working dataset contained:

**87,396 records**

The duplicate-removal step only identifies records that were identical
across all available columns. It does not assume that every duplicate
represented a confirmed data-entry error.

------------------------------------------------------------------------

## 🛠️ Tools & Technologies

  Tool              Purpose
  ----------------- ------------------------------------------------
  **Power BI**      Dashboard development and interactive analysis
  **Power Query**   Data cleaning and transformation
  **DAX**           Measures and calculated fields

------------------------------------------------------------------------

# 📈 Dashboard

## Summary Cards

The dashboard contains four Card visuals:

  Card                         Description
  ---------------------------- -------------------------------------------
  **Total Bookings**           Total number of booking records
  **Cancellation Rate**        Percentage of bookings that were canceled
  **Total Revenue**            Booking-derived revenue calculation
  **Average Daily Rate**      Average Daily Rate
  **Average Length of Stay**   Average number of nights per booking

These Cards provide a quick numerical overview before users explore the
detailed visuals.

------------------------------------------------------------------------

## 1. 📈 Booking Demand Over Time

**Visual:** Line Chart

**Fields:** - X-axis: `Arrival Year` - Y-axis: `Total Bookings`

This visual shows how booking demand changes over time and allows users
to identify changes in booking volume and broader demand patterns.

------------------------------------------------------------------------

## 2. ❌ Cancellation Analysis

**Visual:** Column Chart

This visual shows cancellation rate across different distribution
channels, allowing users to compare cancellation behavior by channel.

------------------------------------------------------------------------

## 3. 👤 Customer Repeat Status (Yes = Repeat, No = New)

**Visual:** Pie / Donut Chart

This visual uses the `is_repeated_guest` field to show the distribution
of bookings between:

-   **Yes = Repeat Guest**
-   **No = New Guest**

It provides a simple view of repeat-guest participation within the
booking data.

------------------------------------------------------------------------

## 4. 📊 Market Segment Analysis

**Visual:** Horizontal Bar Chart

**Fields:** - Y-axis: `market_segment` - X-axis: `Total Bookings`

This visual compares booking volume across different market segments.

------------------------------------------------------------------------

# 🎛️ Interactive Features

The dashboard includes the following slicers:

-   **Hotel**
-   **Arrival Year**
-   **Arrival Month**
-   **Market Segment**
-   **Distribution Channel**

The visuals interact with each other, allowing users to explore
different combinations of the data.

### Reset Filters

A dedicated **Reset Filters** button returns the dashboard to its
default filter state.

------------------------------------------------------------------------

# 🧮 Main DAX Measures

### Total Bookings

``` dax
Total Bookings =
COUNTROWS('hotel_bookings')
```

### Cancellation Rate

``` dax
Cancellation Rate =
DIVIDE(
    CALCULATE(
        COUNTROWS('hotel_bookings'),
        'hotel_bookings'[is_canceled] = 1
    ),
    COUNTROWS('hotel_bookings')
)
```

### Total Revenue

``` dax
Total Revenue =
SUMX(
    'hotel_bookings',
    ('hotel_bookings'[stays_in_weekend_nights] +
     'hotel_bookings'[stays_in_week_nights])
    * 'hotel_bookings'[adr]
)
```

### Average Length of Stay

``` dax
Average Length of Stay =
AVERAGEX(
    'hotel_bookings',
    'hotel_bookings'[stays_in_weekend_nights]
    + 'hotel_bookings'[stays_in_week_nights]
)
```

### Average Lead Time

``` dax
Average Lead Time =
AVERAGE('hotel_bookings'[lead_time])
```

------------------------------------------------------------------------

# ⚠️ Data & Revenue Considerations

The `Total Revenue` measure in this project is a **booking-derived
revenue calculation**, based on:

**Length of Stay × Average Daily Rate**

The dataset does not contain a direct payment or cash-revenue field.
Therefore, this measure should **not** be interpreted as verified actual
revenue received by the hotels.

Similarly, the dataset contains canceled bookings. Unless a visual or
filter specifically excludes them, measures calculated across the full
dataset should be interpreted as characteristics of the **booking
records**, rather than confirmed realized stays or payments.

------------------------------------------------------------------------

# 💡 Business Questions

The dashboard helps answer questions such as:

-   How does booking demand change over time?
-   How does cancellation rate vary across distribution channels?
-   What proportion of bookings comes from repeat guests?
-   Which market segments account for the most bookings?
-   How do these patterns change when different hotels, years, months,
    market segments, or distribution channels are selected?

------------------------------------------------------------------------

# 📁 Project Structure

``` text
hotel-booking-analysis-powerbi/
│
├── README.md
│
└── PowerBI/
    └── Hotel_Booking_Analysis.pbix
```

The original dataset can be referenced through its public source rather
than unnecessarily duplicating the full dataset inside the repository.

------------------------------------------------------------------------

# 🚀 How to Use

1.  Download the `.pbix` file.
2.  Open it with **Power BI Desktop**.
3.  Use the slicers to filter the dashboard.
4.  Interact with the visuals to explore the booking data.
5.  Use **Reset Filters** to restore the default dashboard state.

------------------------------------------------------------------------

# 📚 Dataset Source

**Hotel Booking Demand Dataset**

Antonio, N., de Almeida, A., & Nunes, L. (2019). *Hotel booking demand
datasets.*

The dataset is publicly available and was developed for research and
analysis of hotel booking demand.

------------------------------------------------------------------------

# 👤 Author

**Milad**

Statistics Graduate \| Data Analytics

**Tools:** Power BI · Power Query · DAX
