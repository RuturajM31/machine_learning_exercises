# Business Understanding of the Dataset

## Dataset Overview

This dataset contains digital marketing campaign data.

Each row represents a customer or campaign-related record with customer profile, campaign details, engagement behavior, and conversion results.

The dataset has:

- 8,000 rows
- 20 columns

## Column Groups

### 1. Customer Profile Columns

These columns describe the customer.

| Column | Meaning |
|---|---|
| `CustomerID` | Unique customer identifier |
| `Age` | Age of the customer |
| `Gender` | Gender of the customer |
| `Income` | Customer income |
| `PreviousPurchases` | Number of previous purchases |
| `LoyaltyPoints` | Customer loyalty points |

### 2. Campaign Columns

These columns describe the marketing campaign.

| Column | Meaning |
|---|---|
| `CampaignChannel` | Marketing channel used |
| `CampaignType` | Type or objective of campaign |
| `AdSpend` | Advertising spend |

### 3. Engagement Columns

These columns describe how the user interacted with marketing or website content.

| Column | Meaning |
|---|---|
| `ClickThroughRate` | Rate at which users clicked |
| `WebsiteVisits` | Number of website visits |
| `PagesPerVisit` | Average pages visited |
| `TimeOnSite` | Time spent on the website |
| `SocialShares` | Number of social shares |
| `EmailOpens` | Number of email opens |
| `EmailClicks` | Number of email clicks |

### 4. Technical Columns

These columns are not very useful for modeling.

| Column | Why |
|---|---|
| `CustomerID` | ID column, not a real predictive feature |
| `AdvertisingPlatform` | Appears to be a technical/confidential value |
| `AdvertisingTool` | Appears to be a technical/confidential value |

### 5. Target Columns

These are the output columns.

| Column | Meaning | ML Task |
|---|---|---|
| `ConversionRate` | Numeric conversion rate | Regression |
| `Conversion` | 0/1 conversion result | Classification |

## Modeling Decision

For Day 1 Linear Regression, I will use:

`ConversionRate`

as the target variable.

Reason:

Linear Regression works best when the target is numeric and continuous.

Later, I can use:

`Conversion`

for classification using Logistic Regression.

## Business Questions

This analysis will help answer questions like:

1. Does higher ad spend relate to higher conversion rate?
2. Do email clicks improve conversion performance?
3. Does time on site matter?
4. Which variables have stronger relationship with conversion rate?
5. Can we predict conversion rate using customer and campaign features?

## Important Caution

Regression can show relationships, but it does not automatically prove causation.

For example:

If `AdSpend` and `ConversionRate` are related, that does not prove ad spend directly caused the conversion rate to increase.

Other factors may also be involved:

- campaign quality
- audience targeting
- seasonality
- discounts
- website experience
- brand strength