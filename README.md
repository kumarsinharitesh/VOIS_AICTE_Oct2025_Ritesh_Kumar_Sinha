# VOIS_AICTE_Oct2025_Ritesh_Kumar_Sinha
Overview
This project performs end‑to‑end exploratory data analysis of the NYC Airbnb Open Data using Python in Google Colab, covering data loading, cleaning, feature typing, grouping, visualization, and simple statistical checks to answer domain questions about listings, prices, hosts, and reviews.
Documentation follows common README best practices for data analysis projects so others can understand methods, reproduce results, and extend the work easily.

Tech stack
Python with pandas for data wrangling and summaries, including groupby, sorting, and correlations.

Matplotlib and seaborn for visuals such as bar charts and regression plots with fitted lines.

Google Colab as the execution environment for a quick, dependency‑light workflow.

How to run (Colab)
Upload the CSV to Colab or mount Drive, then read with pandas using low_memory=False for mixed‑typed columns.

Execute cells in order; plotting uses matplotlib/seaborn, which render inline in Colab without extra setup.

Data preparation
Remove duplicate rows with DataFrame.drop_duplicates to ensure unique records.

Clean monetary columns by stripping symbols and commas via Series.str.replace with regex=False before numeric casting.

Rename columns for clarity and cast to numeric, datetime, or string types as appropriate using pandas astype and to_datetime.

Handle obvious text fixes (e.g., standardizing neighborhood names) and optionally drop rows with missing values for strict analyses.

Core analyses
Listing distributions: value_counts and DataFrame/Series operations to summarize room types and neighborhood groups.

Neighborhood insights: groupby on 'neighbourhood group' for counts and means, with sorting to identify leading segments.

Pricing dynamics: compute average price by group and visualize with labeled bar charts to compare across neighborhoods.

Construction year trends: groupby year, mean price, and plot via pandas .plot for quick trend inspection.

Host perspective: top hosts by 'calculated host listings count' using groupby, sum, sort_values, and nlargest for top‑N selection.

Review behavior: compare mean 'review rate number' by host_identity_verified to assess differences across verification status.

Price–fee relationship: compute Pearson correlation with Series.corr and visualize with seaborn regplot for linear trend.

Visualizations produced
Matplotlib bar charts with plt.bar and annotated values via plt.bar_label to display counts and averages on bars.

Seaborn barplot with hue to show average review rates across neighborhood groups segmented by room type, using the default mean estimator.

Seaborn regplot to examine linear relationships between price and service fee and between host listing count and availability.

Axis labels, titles, rotated ticks, and y‑limits configured with pyplot helpers for readability in dashboards and reports.

Example usage snippet
Load data and clean currency fields, then compute room‑type counts for a labeled bar chart.

python
df = pd.read_csv('/content/Airbnb Open Data.csv', low_memory=False)
df['price'] = df['price'].astype(str).str.replace('$','',regex=False).str.replace(',','',regex=False)
df['service fee'] = df['service fee'].astype(str).str.replace('$','',regex=False).str.replace(',','',regex=False)
df['price_$'] = pd.to_numeric(df['price'])
df['service_fee_$'] = pd.to_numeric(df['service fee'])
property_types = df['room type'].value_counts().to_frame('count')
ax = plt.bar(property_types.index, property_types['count'])
plt.bar_label(ax, labels=property_types['count'], padding=4)
plt.xlabel('Room Type'); plt.ylabel('Room Type Count'); plt.title('Property Types and their count')
plt.show()
Key plots/checks
Room types and their frequencies: bar chart with labels to compare category sizes at a glance.

Neighborhood group listing counts: bar chart with rotation and y‑limits for dense category labels.

Average price by neighborhood: sorted bar chart with edge labels for dollar values.

Average price vs construction year: grouped mean line/area from pandas plot for trend direction.

Top 10 hosts by listing count: nlargest after groupby sum for efficient ranking.

Verification vs reviews: grouped mean review rates to compare verified and unverified hosts.

Price–service fee correlation and regplot: numeric correlation and fitted line to quantify and show association.

Conclusion
This analysis highlights the dominance of Entire home/apartment listings, substantial variability in listing counts across neighborhood groups, and a downward association between property construction year and price, as observed in grouped trends and plots from the notebook.
It also surfaces the impact of host identity verification on average review rates and a strong positive association between listing price and service fee, corroborated by correlation metrics and regression visualizations in the workflow.
Future extensions include sentiment analysis on guest reviews to link satisfaction drivers with product and marketing decisions, plus predictive modeling for demand and pricing using regression or machine learning, enabling more robust forecasting and operational planning for short‑term rentals.



If a Markdown file is needed, this text can be saved as README.md in the repo root so that it’s immediately visible in Git hosting interfaces and remains easy to maintain alongside the notebook.
