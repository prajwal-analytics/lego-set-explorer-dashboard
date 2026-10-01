An interactive Power BI dashboard that works like a smart shopping assistant for LEGO sets — filter, compare, and inspect 4,385 sets without scrolling ever again.

Built with Power BI Desktop · Power Query · DAX

📸 The Dashboard

<img width="857" height="480" alt="image" src="https://github.com/user-attachments/assets/a1bf1c86-2643-4ff1-a6ba-bfc0f7ff33cb" />, <img width="860" height="479" alt="image" src="https://github.com/user-attachments/assets/1bb34867-9769-468e-8fb0-44f528791a89" />


🛒 The Problem
Buying a LEGO set today means drowning in options: thousands of sets, wildly different prices, dozens of themes, age recommendations everywhere. Raw LEGO data usually arrives as big Excel tables — boring to read, slow to compare, and easy to misread.

Questions that take forever to answer manually:

Which LEGO set is best for adults?
Which one is expensive — and is it worth the piece count?
What fits a 10-year-old?
💡 The Solution
A product-style dashboard, modeled on the filter-and-compare experience of Amazon or Flipkart:

Filter like a store — dropdown slicers for Theme Group, Theme, and Age Range
Compare in one glance — a clean table with Set Name, Set ID, Theme, Age Range, Pieces, Price, and a shopping-style price band ($ → $$$$$)
Click one set → see its product page — image, price, release year, theme, and age in a detail panel that updates instantly
📊 Features & How They Work
KPI cards that think
Total Sets, Average Price, and Average Pieces update dynamically with every filter and selection — powered by a dedicated DAX Measures table (Total Sets, Total Theme Groups, Average Price, Average Pieces, Average Age).

Smart multi-select handling (the part I'm proud of)
Select one LEGO set and the detail panel shows its exact name, price, year, pieces, and age. Select multiple sets, and Power BI would normally blend their prices and years into misleading averages.

Fix: advanced DAX logic using HASONEVALUE() with custom "Selected" measures (Selected Set Name, Selected Price, Selected Year, Selected Pieces, Selected Age):

1 set selected → exact product details
Multiple selected → clean placeholder values, never wrong numbers
The dashboard stays accurate and trustworthy at the edges — not just in the demo case.

Feature engineering for humans
Age Range: raw ages grouped into 1–4 · 5–9 · 10–17 · Over 18 — so parents and gift-buyers can filter in one click
Price Range: prices grouped into $ · $$ · $$$ · $$$$ · $$$$$ — the same mental model as shopping-site filters
🧹 Data Pipeline (Power Query)
Raw data is messy — like an unorganized room. Before any visual was built:

Fixed data types (price and age arrived as text, not numbers)
Removed unnecessary columns (extra image URLs, minifig counts)
Renamed columns for clarity
Removed rows missing critical values (no price, no image)
Profiled the data to understand price and theme distribution
Final cleaned dataset: 4,385 LEGO sets (sets released since 1970 — each row one set: name, release year, theme & theme group, recommended age, piece count, retail price, image URL).

🛠️ Tech Stack
